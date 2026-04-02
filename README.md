# Social Media Mini App (Spring Boot + JPA)

This project is a backend-focused mini application developed to understand and implement core concepts of Java Persistence API (JPA) in a practical setting. The application models a simplified social media system with users, profiles, posts, and groups, emphasizing data relationships and persistence behavior.

---

## Overview

The application supports the following functionalities:

* A user can have a profile (one-to-one relationship)
* A user can create multiple posts (one-to-many relationship)
* Users can be part of multiple groups (many-to-many relationship)

The primary goal of this project is to gain a strong understanding of how entities interact with each other and how these relationships are managed in a database using JPA.

---

## Key Concepts Implemented

### 1. Entity Relationship Mapping

The project demonstrates multiple types of relationships:

* One-to-One: SocialUser and SocialProfile
* One-to-Many: SocialUser and Post
* Many-to-Many: SocialUser and SocialGroup

It also explores the use of `@JoinColumn` and `mappedBy` to define owning and inverse sides of relationships.

---

### 2. Cascading

Cascading operations were implemented using:

```java
cascade = {CascadeType.PERSIST, CascadeType.MERGE}
```

This ensures that persistence and update operations on the parent entity are propagated to the associated child entity. The project highlights that cascading does not automatically establish relationships; explicit linking of entities is required before saving.

---

### 3. Fetch Strategies

The application explores different fetch types:

* Lazy Fetching
* Eager Fetching

This helps in understanding performance implications and controlling how and when related data is loaded from the database.

---

### 4. Handling Circular References

Bidirectional relationships can lead to infinite recursion during JSON serialization. This issue was addressed using:

```java
@JsonIgnore
```

This ensures that API responses remain stable and do not result in serialization errors.

---

### 5. Owning vs Inverse Side

A key concept implemented in this project is identifying the owning side of a relationship. The entity containing the `@JoinColumn` annotation is responsible for managing the relationship in the database.

In this case:

* SocialProfile is the owning side
* SocialUser is the inverse side

---

## Technology Stack

* Spring Boot
* Hibernate / JPA
* H2 Database
* Java
* Postman (for API testing)

---

## Sample API Request

### Create a User with Profile

```json
{
  "socialProfile": {
    "description": "Learning never stops"
  }
}
```

---

## Challenges Faced

* Handling null foreign keys due to improper relationship setup
* Understanding why cascade operations did not behave as expected
* Resolving circular reference issues during JSON serialization
* Distinguishing between owning and inverse sides of relationships

---

## Key Learnings

* Relationships must be explicitly defined and maintained on the owning side
* Cascade operations only propagate actions; they do not establish relationships
* Proper understanding of fetch strategies is important for performance optimization
* Serialization issues must be handled carefully in bidirectional mappings

---

## Future Enhancements

* Introduce DTOs to decouple API responses from entity models
* Implement authentication and authorization
* Add pagination and filtering for posts
* Migrate to a production-grade database such as MySQL or PostgreSQL
* Develop a frontend interface using a modern framework

---

## Conclusion

This project focuses on building a strong foundation in JPA by working with real-world relationship mappings and persistence behavior. It provides practical insights into how backend systems manage complex data interactions and ensures a deeper understanding of core backend development principles.
