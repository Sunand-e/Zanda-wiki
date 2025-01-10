Welcome to the Zanda360 Rails API repository!

 Zanda360 is a comprehensive learning management system (LMS) designed to facilitate the creation, management, and distribution of training/educational content. This repository contains the source code for the Zanda360 Rails API.

## Features

- **Multiple Tenancies**: Support for multiple tenants, allowing separate management of users and content for different organizations.
- **Course Builder**: Create courses with sections, lessons, and quizzes.
- **Quiz Builder**: Build quizzes with single and multiple-choice questions.
- **Resource Library**: Manage documents, workshops, webinars, podcasts, process flows, and snapshots.
- **User Roles & Capabilities**: Manage user roles and content/feature access using capabilities.
- **Groups/Organisations**: Organize users within tenants.
- **User Actions on Content Pieces**: Track user interactions with content.
- **Reporting**: Generate reports on course progress and user performance.

## Local Setup

To set up the application locally, follow these steps:

1. Create the local Docker containers:
    ```sh
    docker-compose up -d
    ```

2. That's it.

## Description

- **Gemfile**: Describes the gem dependencies required to execute associated Ruby code.
- **Gemfile.lock**: Records the exact versions of gems installed, ensuring consistency across different environments.

## GraphQL Integration

MemberHub uses GraphQL for API interactions. For more information on GraphQL and its implementation with Rails, refer to the following resources:
- [GraphQL Ruby](https://graphql-ruby.org/): A Ruby gem for building GraphQL APIs with Ruby.
- [GraphQL on Rails](https://evilmartians.com/chronicles/graphql-on-rails-1-from-zero-to-the-first-query)
