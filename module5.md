# Module 5 – Reflection on the Experience

## Overview  
This module provided a valuable hands-on experience in understanding the foundational concepts of **Online Public Access Catalogs (OPAC)** and **cataloging modules** within library systems. The assignment emphasized both the technical and conceptual frameworks required to build a basic, functioning library catalog system.

---

## What I Learned

### OPAC and Relational Databases  
One of the most intuitive parts of the assignment was understanding how OPAC interacts with a **relational database** to manage bibliographic data. The **textbook** clearly outlined how to design a basic database structure and interact with it using SQL.  

Using **PHP and MySQL**, I found it surprisingly straightforward to insert and retrieve data. This process solidified my understanding of how web-based databases operate and how libraries leverage these systems to manage collections efficiently.

---

### Technical Challenges  

While the initial database and form setup were manageable, ensuring **data security** and **input validation** required further research. Specifically:

- I encountered difficulties securing PHP forms against **SQL injection**.
- I wasn’t initially familiar with best practices for preventing this vulnerability.
  
To solve this, I studied the use of **prepared statements** in PHP, which I implemented to sanitize user input and prevent malicious data entry. Additionally, I had to be attentive to **data types**, especially for fields like copyright year, as mishandling these caused query errors.

---

## Key Takeaways  

- **Attention to detail is essential.** Small errors—like improper validation or data type mismatches—can lead to major issues in data integrity or system security.
- The assignment reinforced the need for **rigorous testing**, especially when working with web forms and databases.
- I gained appreciation for the **ongoing maintenance** required in real-world library systems, especially in securing inputs and updating features.

---

## Real-World Connections  

Although our system was basic, the core functions—cataloging, querying, and user interaction—mirror those of **professional library management systems**. Real-world OPACs involve:

- Advanced search functionalities  
- User authentication  
- Role-based access control  
- Scalable databases

This project helped me visualize how libraries maintain and update their collections through digital systems and highlighted the **complexity behind seemingly simple interfaces**.

---

## Final Thoughts  

This was an excellent introduction to the core concepts of **systems librarianship**, especially in bridging theory with practical coding. The hands-on experience gave me a better understanding of both **technical workflows** and the **real-world relevance** of managing digital library systems.

---

## Submission Links  

- 🔗 **GitHub Repository:** [View Commit](https://github.com/clcjo20/syslib2025/commit/9f9ebda5182f1657918fdf2dd17a3af9e05fc4b7)  
- 🖥️ **OPAC Page:** [http://34.134.86.249/mylibrary.html](http://34.134.86.249/mylibrary.html)  
- 🗃️ **Cataloging Module:** [http://34.134.86.249/cataloging/](http://34.134.86.249/cataloging/)
