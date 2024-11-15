# Database-design
This project focuses on designing and normalising a relational database for a hardware company, emphasising efficiency, clarity, and scalability. It employs Entity-Relationship Diagrams (ERD) and normalisation techniques to manage entities such as employees, products, branches, and sales records, ensuring data integrity while minimising redundancy.



### Database Design and Entity Relationships

#### 1. Entity-Relationship Diagram (ERD)
The ERD models key entities and their relationships, facilitating data organisation and operations. Major components include:

1. **Employee Table**:
   - Attributes: `employee id`, `name`, `year of hire`.
   - Acts as the superclass for two subclasses: **Branch Manager** and **Salesperson**.
   - Enhances user interaction with fields like `name` for clarity.

2. **Branch Manager**:
   - Role identifier with attributes like `manager number`.
   - Participates in a recursive relationship (`Manages`) with branches, representing administrative hierarchies.

3. **Salesperson**:
   - Core entity with attributes `salesperson number` and `commission percentage`.
   - Connected to multiple entities like products, sales records, and customers.

4. **Branch**:
   - Attributes: `branch id`, `location`.
   - Central to all relationships, categorising employees, offices, and operations by branch.
   - Connected to employees (`Employs`) and offices (`Has`).

5. **Office**:
   - Attributes: `office number`, `telephone number`, `room size`.
   - Directly related to branches and salespersons, enabling spatial allocation.

6. **Product and Manufacturer**:
   - Products: Attributes like `product number`, `name`, `unit price`, and `description`.
   - Manufacturers: Includes `manufacturer id` and `name`.
   - Relationships: Products are linked to manufacturers (`Produced by`) and sales records (`Product Sold`).

7. **Customer and Customer Employee**:
   - Customer: Attributes like `customer id`, `name`, and `location`.
   - Customer Employee: Represents workers hired by customers.
   - Relationships: Customers are served by salespersons and employ customer employees.

8. **Sales Record**:
   - Tracks transactions through relationships like `Product Sold` and `Seller`.
   - Attributes include transactional details such as product, quantity, and salesperson information.

---

### Normalisation Process

#### 1. First Normal Form (1NF)
- Removed repeating groups by splitting rows with composite fields into distinct rows.
- Introduced a unique identifier (`transaction number`) to ensure atomicity.
- Ensured each field hosts a single type of data, resolving insertion and deletion anomalies.

#### 2. Second Normal Form (2NF)
- Eliminated partial dependencies by creating separate tables:
  - **Salesperson Table**: Contains `salesperson number`, `name`, `commission percentage`, and other details.
  - **Product Table**: Attributes include `product number`, `name`, and `unit price`.
- Reduced redundancy, enabling efficient updates without blank or inconsistent fields.

#### 3. Third Normal Form (3NF)
- Removed transitive dependencies:
  - `Manager` depended on `Department Number`.
  - Created a **Manager Table** to link `department number` and `manager`.
- Achieved a lossless compression, significantly reducing table size while retaining data integrity.

---

### Key Design Decisions

1. **Scalability**:
   - Integer-based primary keys (`int`) allow for large datasets.
   - Efficient use of data types like `varchar` for string attributes, ensuring compact storage.

2. **Data Integrity**:
   - Relationships like one-to-one (`Manages`) and one-to-many (`Employs`, `Works in`) ensure clear data flow.
   - Constraints like exclusive subclasses (e.g., a Branch Manager cannot also be a Salesperson) uphold logical consistency.

3. **User-Friendliness**:
   - Fields like `name` and `description` were added for clarity, simplifying data interpretation for users.

4. **Efficiency**:
   - Attributes like `room size` in offices use compact data types (`tinyint`), conserving storage.
   - Relationships such as `Product Sold` streamline transactional tracking.

---

### Challenges and Assumptions

1. **Challenges**:
   - Designing a recursive relationship between Branch Managers and Branches.
   - Balancing normalisation to avoid excessive table fragmentation.

2. **Assumptions**:
   - Each department has exactly one manager.
   - All tools of the same type are of equal value.
   - Rows in the dataset maintain attribute correlation.

---

### Conclusion

This database design exemplifies robust data management, combining ERD modeling with comprehensive normalisation to support scalability, clarity, and operational efficiency. It provides a structured framework for hardware company operations, optimising data handling and future-proofing the system for expansion.
