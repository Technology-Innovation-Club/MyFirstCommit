openapi: 3.0.0
info:
  title: Infoverse API
  version: 1.0.0
  description: API documentation for Infoverse project
components:
  securitySchemes:
    bearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT
security:
  - bearerAuth: []
paths:
  /api/auth/test:
    post:
      summary: Test route (for sanity checks)
      tags:
        - Auth
      responses:
        200:
          description: Returns ok
  /api/auth/register:
    post:
      summary: Register a new user
      tags:
        - Auth
      requestBody:
        required: true
        content:
          application/json:
            example:
              name: John Doe
              email: john@example.com
              password: strongpassword123
      responses:
        201:
          description: User registered successfully
        400:
          description: Email already in use
  /api/auth/login:
    post:
      summary: Login a user
      tags:
        - Auth
      requestBody:
        required: true
        content:
          application/json:
            example:
              email: john@example.com
              password: strongpassword123
      responses:
        200:
          description: Login successful, returns JWT token
        401:
          description: Invalid credentials
  /api/courses:
    get:
      summary: Get paginated list of courses
      tags:
        - Courses
      parameters:
        - in: query
          name: page
          schema:
            type: integer
          default: 1
        - in: query
          name: limit
          schema:
            type: integer
          default: 10
      responses:
        200:
          description: List of courses with pagination
    post:
      summary: Create a new course
      tags:
        - Courses
      security:
        - bearerAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              required:
                - title
                - description
                - price
              properties:
                title:
                  type: string
                description:
                  type: string
                price:
                  type: number
                thumbnailUrl:
                  type: string
                syllabus:
                  type: array
                  items:
                    type: object
                    properties:
                      title:
                        type: string
                      contentType:
                        type: string
                        enum:
                          - video
                          - text
                          - quiz
                      contentUrl:
                        type: string
      responses:
        201:
          description: Course created successfully
        400:
          description: Validation error
        403:
          description: Forbidden (not instructor)
  /api/courses/{id}:
    get:
      summary: Get a course by ID
      tags:
        - Courses
      parameters:
        - in: path
          name: id
          required: true
          schema:
            type: string
      responses:
        200:
          description: The course data
        404:
          description: Course not found
    put:
      summary: Update a course
      tags:
        - Courses
      security:
        - bearerAuth: []
      parameters:
        - in: path
          name: id
          required: true
          schema:
            type: string
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                title:
                  type: string
                description:
                  type: string
                price:
                  type: number
      responses:
        200:
          description: Course updated successfully
        400:
          description: Validation error
        403:
          description: Forbidden (not instructor)
        404:
          description: Course not found
    delete:
      summary: Delete a course
      tags:
        - Courses
      security:
        - bearerAuth: []
      parameters:
        - in: path
          name: id
          required: true
          schema:
            type: string
      responses:
        200:
          description: Course deleted
        403:
          description: Forbidden (not instructor)
        404:
          description: Course not found
  /api/courses/{courseId}/enroll:
    post:
      summary: Enroll the authenticated user in a course
      tags:
        - Enrollments
      security:
        - bearerAuth: []
      parameters:
        - in: path
          name: courseId
          required: true
          schema:
            type: string
      responses:
        201:
          description: Enrollment successful
        400:
          description: Already enrolled or validation error
        401:
          description: Unauthorized
  /api/users/me/courses:
    get:
      summary: Get all courses the user is enrolled in
      tags:
        - Enrollments
      security:
        - bearerAuth: []
      responses:
        200:
          description: List of enrolled courses
          content:
            application/json:
              schema:
                type: object
                properties:
                  data:
                    type: array
                    items:
                      type: object
                      properties:
                        courseId:
                          type: string
                        title:
                          type: string
                        enrolledAt:
                          type: string
                          format: date-time
  /api/courses/{courseId}/enrollments:
    get:
      summary: Get all enrollments for a course (instructor only)
      tags:
        - Enrollments
      security:
        - bearerAuth: []
      parameters:
        - in: path
          name: courseId
          required: true
          schema:
            type: string
      responses:
        200:
          description: List of enrollments for course
        401:
          description: Unauthorized
        403:
          description: Forbidden
  /api/enrollments/{enrollmentId}:
    put:
      summary: Update an enrollment status (instructor only)
      tags:
        - Enrollments
      security:
        - bearerAuth: []
      parameters:
        - in: path
          name: enrollmentId
          required: true
          schema:
            type: string
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                status:
                  type: string
                  enum:
                    - active
                    - completed
                    - dropped
      responses:
        200:
          description: Enrollment status updated
        401:
          description: Unauthorized
        403:
          description: Forbidden
  /api/courses/{courseId}/drop:
    delete:
      summary: Drop a course the user is enrolled in
      tags:
        - Enrollments
      security:
        - bearerAuth: []
      parameters:
        - in: path
          name: courseId
          required: true
          schema:
            type: string
      responses:
        200:
          description: Course dropped successfully
        401:
          description: Unauthorized
  /api/users/me/profile:
    get:
      summary: Get current user's profile
      tags:
        - Users
      security:
        - bearerAuth: []
      responses:
        200:
          description: User profile retrieved
          content:
            application/json:
              schema:
                type: object
                properties:
                  id:
                    type: string
                  name:
                    type: string
                  email:
                    type: string
        401:
          description: Unauthorized
    put:
      summary: Update current user's profile
      tags:
        - Users
      security:
        - bearerAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                name:
                  type: string
                email:
                  type: string
      responses:
        200:
          description: User profile updated
        400:
          description: Validation error
        401:
          description: Unauthorized
tags:
  - name: Auth
    description: User authentication
  - name: Courses
    description: Course management and retrieval
  - name: Enrollments
    description: Course enrollment operations
  - name: Users
    description: User profile operations
