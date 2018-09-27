# docker-rails-template
Rails + MySQL environment settings for development.

## Usage
1. Copy this repository to project directory.  
2. Create and edit env file
```
cp common.env.sample common.env
# and edit
```
3. Build.
```
docker-compose build
```
4. Create Rails project on working directory of app.
```
docker-compose run --rm app rails new . --force --database=mysql --skip-bundle
```
5. Edit app/config/database.yml.
```
password: <%= ENV.fetch("MYSQL_PASSWORD") %>
host: db
# and other settings like charset
```
6. Install gems for Rails
```
docker-compose run --rm app bundle install
```
7. Create db
```
docker-compose run --rm app rails db:create
```
8. Up
```
docker-compose up
```
9. Done

http://localhost:3000

## Adding gems
Updating Gemfile and ```docker-compose build``` doesn't work because image's bundle directory is hidden by the mounted volume when the container runs.  
Do ```docker-compose run --rm app bundle install``` to install gems into the mounted volume.
