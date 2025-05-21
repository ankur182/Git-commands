Thanks! Based on your JSON data and your use of H2 database with Liquibase, I’ll now help you generate a Liquibase changelog that:

1. Creates employer and employee tables (One-to-Many).


2. Inserts the initial data into both tables (with relationships preserved).




---

Liquibase Changelog: db.changelog-master.xml

<databaseChangeLog
        xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog
        http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-3.1.xsd">

    <!-- Create Employer Table -->
    <changeSet id="1" author="dev">
        <createTable tableName="employer">
            <column name="employer_id" type="BIGINT">
                <constraints primaryKey="true" nullable="false"/>
            </column>
            <column name="pan_no" type="VARCHAR(20)"/>
            <column name="est_date" type="DATE"/>
            <column name="location" type="VARCHAR(100)"/>
        </createTable>
    </changeSet>

    <!-- Create Employee Table -->
    <changeSet id="2" author="dev">
        <createTable tableName="employee">
            <column name="emp_id" type="BIGINT">
                <constraints primaryKey="true" nullable="false"/>
            </column>
            <column name="name" type="VARCHAR(100)"/>
            <column name="age" type="INT"/>
            <column name="salary" type="DECIMAL(10,2)"/>
            <column name="employer_id" type="BIGINT"/>
        </createTable>
    </changeSet>

    <!-- Foreign Key -->
    <changeSet id="3" author="dev">
        <addForeignKeyConstraint 
            baseTableName="employee"
            baseColumnNames="employer_id"
            referencedTableName="employer"
            referencedColumnNames="employer_id"
            constraintName="fk_emp_employer"/>
    </changeSet>

    <!-- Insert Employers -->
    <changeSet id="4" author="dev">
        <insert tableName="employer">
            <column name="employer_id" valueNumeric="1"/>
            <column name="pan_no" value="ABC023"/>
            <column name="est_date" valueDate="2020-01-01"/>
            <column name="location" value="Delhi"/>
        </insert>
        <insert tableName="employer">
            <column name="employer_id" valueNumeric="2"/>
            <column name="pan_no" value="ABC045"/>
            <column name="est_date" valueDate="2000-07-10"/>
            <column name="location" value="Mumbai"/>
        </insert>
        <insert tableName="employer">
            <column name="employer_id" valueNumeric="3"/>
            <column name="pan_no" value="KL8232"/>
            <column name="est_date" valueDate="2008-02-10"/>
            <column name="location" value="Kolkata"/>
        </insert>
    </changeSet>

    <!-- Insert Employees -->
    <changeSet id="5" author="dev">
        <insert tableName="employee">
            <column name="emp_id" valueNumeric="1"/>
            <column name="name" value="Ankur"/>
            <column name="age" valueNumeric="20"/>
            <column name="salary" valueNumeric="60000.0"/>
            <column name="employer_id" valueNumeric="1"/>
        </insert>
        <insert tableName="employee">
            <column name="emp_id" valueNumeric="2"/>
            <column name="name" value="Anjali"/>
            <column name="age" valueNumeric="18"/>
            <column name="salary" valueNumeric="30000.0"/>
            <column name="employer_id" valueNumeric="1"/>
        </insert>
        <insert tableName="employee">
            <column name="emp_id" valueNumeric="3"/>
            <column name="name" value="Rajiv"/>
            <column name="age" valueNumeric="28"/>
            <column name="salary" valueNumeric="70000.0"/>
            <column name="employer_id" valueNumeric="1"/>
        </insert>

        <insert tableName="employee">
            <column name="emp_id" valueNumeric="4"/>
            <column name="name" value="Ritik"/>
            <column name="age" valueNumeric="22"/>
            <column name="salary" valueNumeric="50000.0"/>
            <column name="employer_id" valueNumeric="2"/>
        </insert>
        <insert tableName="employee">
            <column name="emp_id" valueNumeric="5"/>
            <column name="name" value="Riya"/>
            <column name="age" valueNumeric="27"/>
            <column name="salary" valueNumeric="45000.0"/>
            <column name="employer_id" valueNumeric="2"/>
        </insert>

        <insert tableName="employee">
            <column name="emp_id" valueNumeric="6"/>
            <column name="name" value="Aditya Singh"/>
            <column name="age" valueNumeric="29"/>
            <column name="salary" valueNumeric="80000.0"/>
            <column name="employer_id" valueNumeric="3"/>
        </insert>
    </changeSet>

</databaseChangeLog>


---

How to Use This File

1. Place it in src/main/resources/db/changelog/db.changelog-master.xml.


2. Update your application.properties:



spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=
spring.jpa.hibernate.ddl-auto=none
spring.liquibase.change-log=classpath:db/changelog/db.changelog-master.xml


---

Would you like me to generate Java @Entity classes as well for Employer and Employee?
