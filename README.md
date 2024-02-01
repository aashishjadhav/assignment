CREATE TABLE Registration (
    ID INT PRIMARY KEY AUTO_INCREMENT,
    Name VARCHAR(255) NOT NULL,
    Email VARCHAR(255) NOT NULL,
    DateOfBirth DATE,
    -- Add additional fields as needed
);


import mysql.connector

# Connect to MySQL database
db = mysql.connector.connect(
    host="localhost",
    user="your_username",
    password="your_password",
    database="your_database"
)
cursor = db.cursor()

# Create a new record
def create_record(name, email, dob):
    sql = "INSERT INTO Registration (Name, Email, DateOfBirth) VALUES (%s, %s, %s)"
    values = (name, email, dob)
    cursor.execute(sql, values)
    db.commit()
    return cursor.lastrowid

# Retrieve records
def retrieve_records():
    sql = "SELECT * FROM Registration"
    cursor.execute(sql)
    return cursor.fetchall()

# Update an existing record
def update_record(id, name, email, dob):
    sql = "UPDATE Registration SET Name = %s, Email = %s, DateOfBirth = %s WHERE ID = %s"
    values = (name, email, dob, id)
    cursor.execute(sql, values)
    db.commit()

# Delete a record
def delete_record(id):
    sql = "DELETE FROM Registration WHERE ID = %s"
    cursor.execute(sql, (id,))
    db.commit()

# Usage example
record_id = create_record("John Doe", "john@example.com", "1990-01-01")
print("New record ID:", record_id)

records = retrieve_records()
for record in records:
    print(record)

update_record(record_id, "Jane Doe", "jane@example.com", "1985-05-05")

records = retrieve_records()
for record in records:
    print(record)

delete_record(record_id)
