# Diagrams as Code: Streamlining ERD Creation for Data Engineers
As a Data Engineer in a fast-paced company, you know that Entity Relationship Diagrams (ERDs) are essential for documenting and communicating database structures. However, traditional no-code tools often fall short in terms of capabilities and can lead to time-consuming layout tweaks, and become painful to maintain as the data structures change over time. That's where Diagrams as Code comes in, offering a more efficient and developer-friendly approach to creating ERDs.

Diagrams as Code allows you to build diagrams using a simple and intuitive syntax, which can be easily version-controlled and integrated into your existing development workflow. This means that you can treat your diagrams just like any other piece of code - with revision history, collaboration, and easy updates.

One powerful tool for creating Diagrams as Code is Mermaid. Mermaid is a JavaScript-based diagramming and charting tool that uses a simple markdown-like syntax. It supports various diagram types, including flowcharts, sequence diagrams, class diagrams, and of course, ERDs.

## Installing Mermaid
While Mermaid can be run directly from their website with a live editor, having a cli version installed allows you to link recreation of diagrams into your CI/CD tool, allowing for a further level of automation.

Mermaid can be installed locally using npm, and it's simple:
```
npm install @mermaid-js/mermaid-cli
./node_modules/.bin/mmdc -h
```

This assumes you have npm installed. If not, I'll refer you to the npm docs here.

## Creating Your First Diagram
Mermaid uses `*.mmd` files (Mermaid Markdown?), which is a simple plain text format. Let's dive into an example of a simple diagram:
```
erDiagram
    sale {
        id int PK
        employee_id int FK
        client_id int FK
        date datetime
        region varchar
        sale numeric
    }
    employee {
        id int PK
        first_name varchar
        last_name varchar
        department_id int FK
    }
    client {
        id int PK
        first_name varchar
        last_name varchar
    }
    department {
        id int PK
        department varchar
    }

    department ||--o{ employee : contains
    employee ||--o{ sale : assists
    client ||--|{ sale : creates
```

Save this file as `erd.mmd`, and then run the following command:
```
mmdc -i erd.mmd -o erd.png -t dark -b transparent
```
You'll find that an `erd.png` file has been created in the folder. It looks like this:

![](https://github.com/nydasco/diagrams_as_code/blob/23b1e2bfea5e63661347ab55400ab590d16f89bd/erd.png)

This is the same simple database that I've used in my Introduction to SQL articles.

## Code Walk-Thru
In this example, we define four entities: sale, client, employee, and department. Within each of these, we define the fields, field types, and the primary and foreign keys.
```
sale {
    id int PK
    employee_id int FK
    client_id int FK
    date datetime
    region varchar
    sale numeric
}
```
We also specify the relationships between the entities:
```
department ||--o{ employee : contains
employee ||--o{ sale : assists
client ||--|{ sale : creates
```
- a department contains zero or many employees
- an employee assists on zero or many sales
- a client creates one or many sales

Mermaid takes care of the layout and formatting, allowing you to focus on the content and structure of your ERD. You can easily embed this code into your documentation, such as your solution design docs or wiki pages, and the diagram will be rendered automatically.

One of the great advantages of using Diagrams as Code is that changes can be easily made and propagated. If your database structure evolves, you can simply update the Mermaid code and the diagram will reflect the changes. This eliminates the need for manual layout adjustments and ensures that your documentation stays up-to-date with your database.

Additionally, by storing your diagrams as code, you can leverage version control systems like Git. This allows you to track changes, collaborate with team members, and revert to previous versions if needed. Integration with CI/CD pipelines is also possible, enabling automatic diagram updates as part of your development process.

---

In conclusion, Diagrams as Code, and tools like Mermaid, offer Data Engineers a more efficient and developer-friendly way to create and maintain ERDs. By treating diagrams as code, you can streamline your documentation process, keep your diagrams in sync with your database, and collaborate more effectively with your team. Give Diagrams as Code a try and see how it can improve your workflow!
