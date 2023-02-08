# Cloud Engineer Learning Path
A Cloud Engineer plans, configures, sets up, and deploys cloud solutions.

## Overview
Google Cloud is a suite of cloud services hosted on Google's infrastructure. From computing and storage, to data analytics, machine learning, and networking, Google Cloud offers a wide variety of services and APIs that can be integrated with any cloud-computing application or project, from personal to enterprise-grade.

## Open Google console
This button opens the Cloud console: the web console and central development hub for Google Cloud. You will do the majority of your work in Google Cloud from this interface.

## Project ID
A Google Cloud project is an organizing entity for your Google Cloud resources. It often contains resources and services; for example, it may hold a pool of virtual machines, a set of databases, and a network that connects them together. Projects also contain settings and permissions, which specify security rules and who has access to what resources.

A Project ID is a unique identifier that is used to link Google Cloud resources and APIs to your specific project. Project IDs are unique across Google Cloud: there can be only one qwiklabs-gcp-xxx...., which makes it globally identifiable.

## Username and Password
These credentials represent an identity in the Cloud Identity and Access Management (Cloud IAM) service. This identity has access permissions (a role or roles) that allow you to work with Google Cloud resources in the project you've been allocated. googlexxxxxx_student@qwiklabs.net, is a Cloud IAM identity.

# Projects in the Cloud console

A Google Cloud project is an organizing entity for your Google Cloud resources. It often contains resources and services; for example, it may hold a pool of virtual machines, a set of databases, and a network that connects them together. Projects also contain settings and permissions, which specify security rules and who has access to what resources.

Your project has a name, number, and ID. These identifiers are frequently used when interacting with Google Cloud services.

It's not uncommon for large enterprises or experienced users of Google Cloud to have dozens to thousands of Google Cloud projects. Organizations use Google Cloud in different ways, so projects are a good method for organizing cloud computing services (by team or product, for example.)

### Google cloud Project

An organizing entity for anything you build with Google Cloud.

### Menu and services

The navigation menu: Offers quick access to the platform's services and also outlines its offerings.

[This link](https://cloud.google.com/products#top_of_page) takes you to documentation that covers each of these categories in more detail.

Or you can touch the three horizontal bars of the left-upper corner menu to see by category all services.

## Roles and permissions
In addition to cloud computing services, Google Cloud also contains a collection of permissions and roles that define who has access to what resources. You can use the [Cloud Identity and Access Management (Cloud IAM)](https://cloud.google.com/iam/) service to inspect and modify these roles and permissions.

[Here](https://cloud.google.com/iam/docs/understanding-roles/#primitive%5C_roles) you can see basic roles or more customized ones.
For example, As an editor, you can create, modify, and delete Google Cloud resources. However, you can't add or delete members from Google Cloud projects. 

## APIs and services
Google Cloud APIs are a key part of Google Cloud. Like services, the 200+ APIs, in areas that range from business administration to machine learning, all easily integrate with Google Cloud projects and applications.

APIs are application programming interfaces that you can call directly or via the client libraries. Cloud APIs use resource-oriented design principles as described in the [API Design Guide](https://cloud.google.com/apis/design/).

Most Cloud APIs provide you with detailed information on your project’s usage of that API, including traffic levels, error rates, and even latencies, which helps you quickly triage problems with applications that use Google services.

On the Navigation menu (Navigation menu), click APIs & Services > Library. The left pane, under the header Category, displays the different categories available. **This is the most friendly way to see the APIs and librarys that GCP has for you**

In the API search bar, type Dialogflow, and then click Dialogflow API. The Dialogflow description page opens.

The Dialogflow API allows you to build rich conversational applications (e.g., for Google Assistant) without having to understand the underlying machine learning and natural language schema.

[API explorer](https://developers.google.com/apis-explorer/#p/)

