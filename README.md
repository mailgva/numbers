# The web-server that provides interesting facts about numbers.
Requirements:
1. Server must accept an integer as input.
2. Server must use external Numbers service http://numbersapi.com/ to retrieve facts about accepted number.
3. Provide API to submit a number and retrieve result (text info about the number). Recently requested numbers should be stored in cache.
4. Provide metrics API to retrieve the following usage information: 10 most popular numbers (the ones that get requested most often), average latency of the Numbers service, average success rate of the Numbers service.
   Ideal solution would use Spring, Postgres and provide basic documentation.

# Application realized as web-server using REST (JSON). 
Technologies:
- Java 15
- Maven  
- Spring 5.3.2 (no boot)
- Hibernate 5.4.26.Final
- Jackson 2.12.0
- PostgreSQL 42.2.18

App not contains:
- tests
- docker image

# Tutorial
1. Get from git: **git clone https://github.com/mailgva/numbers** 
2. Execute  **mvn clean install**. Will create **numbers.war** file. 
3. You need installed **PostgreSQL** (default port) and database called **numbers**
   - login **user**
   - password **password** 
4. Launch Tomcat.
5. Deploy **numbers.war**.
6. Enjoy app :)

# Available URLs:
1. **/api/v1/fact/{number}** - to get number fact 
2. **/api/v1/fact/{number}/{type}** - to get number fact by type ("trivia", "math", "date", "year")
3. **/api/v1/cachefact/{number}** - to get number fact with using cache
4. **/api/v1/cachefact/{number}/{type}** - to get number fact by type using cache ("trivia", "math", "date", "year")
5. **/api/v1/mostpopular/** - to get 10 most popular numbers
6. **/api/v1/avglatency/** - to get average average latency of the Numbers service
7. **/api/v1/successrate/** - to get average success rate of the Numbers service

Example:
curl http://localhost:8080/numbers/api/v1/fact/11 -H "Accept: application/json"
curl http://localhost:8080/numbers/api/v1/fact/1970/year -H "Accept: application/json"
curl http://localhost:8080/numbers/api/v1/mostpopular/ -H "Accept: application/json"
curl http://localhost:8080/numbers/api/v1/avglatency/ -H "Accept: application/json"
curl http://localhost:8080/numbers/api/v1/successrate/ -H "Accept: application/json"
