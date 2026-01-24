# Glossary for Non-Coders

**Plain English definitions for technical terms** you'll encounter in vibe coding.

---

## A

### API (Application Programming Interface)
**Plain English:** A way for two programs to talk to each other. Like a waiter in a restaurant - you (the customer) tell the waiter what you want, the waiter tells the kitchen, and the kitchen sends your food back through the waiter.

**Example:** When your app needs weather data, it asks the Weather API: "What's the weather in Seattle?" and gets back "72°F, sunny."

### Authentication
**Plain English:** Proving who you are. Like showing your ID at a bar.

**Example:** Logging in with your email and password.

### Authorization
**Plain English:** Proving what you're allowed to do. Like having a VIP pass that lets you backstage.

**Example:** Admins can delete posts; regular users can only delete their own.

---

## B

### Backend
**Plain English:** The parts of the program users can't see - the kitchen of a restaurant. Handles data storage, business logic, and talking to other services.

**Example:** When you submit a form, the backend saves it to the database and sends a confirmation email.

### Bounded Context
**Plain English:** A clearly defined area of your product with its own vocabulary and rules. Like different departments in a company - "customer" means something different to Sales vs. Support.

**Example:** In an e-commerce app, "Order" in the Checkout context (shopping cart) is different from "Order" in the Fulfillment context (shipping).

---

## C

### CI/CD (Continuous Integration / Continuous Deployment)
**Plain English:** Automated testing and deployment. Like having a robot that checks your homework and mails it for you.

- **CI:** Every time you save code, tests run automatically
- **CD:** If tests pass, code automatically goes live

### Component
**Plain English:** A reusable building block of your product. Like LEGO pieces that snap together.

**Example:** A "Login Form" component that's used on both the website and mobile app.

### Context Window
**Plain English:** How much an AI can "remember" in a conversation. Like a person with limited short-term memory - they can only hold so much at once.

**Example:** If you have a 10-page document and a 2-page context window, the AI can only "see" 2 pages at a time.

### CRUD
**Plain English:** Create, Read, Update, Delete - the four basic things you do with data. Like a notebook where you can add pages, read pages, edit pages, and tear out pages.

---

## D

### Database
**Plain English:** A place to store data permanently. Like a filing cabinet that your program can search instantly.

**Types:**
- **SQL databases (PostgreSQL):** Data in tables with rows and columns, like Excel
- **NoSQL databases (MongoDB):** Data in documents, like JSON files in folders

### Dependency
**Plain English:** Code someone else wrote that your code needs to work. Like ingredients in a recipe.

**Example:** If your app shows charts, you might use the "Recharts" dependency instead of building charts from scratch.

### Deployment
**Plain English:** Putting your code somewhere users can access it. Like publishing a book so people can buy it.

**Example:** Your website goes from running on your laptop to running on servers that anyone can visit.

### Domain
**Plain English:** The real-world problem area your software addresses. Not the code, but the business concepts.

**Example:** For a ride-sharing app, the domain includes: rides, drivers, passengers, routes, payments.

---

## E

### Edge Function
**Plain English:** A small program that runs in the cloud, close to your users. Like having mini-kitchens in every city instead of shipping all food from one central kitchen.

**Example:** Clairu's `coach-reply` edge function runs on Supabase's servers, not your phone.

### Endpoint
**Plain English:** A specific URL where your API listens for requests. Like a specific counter at a government office.

**Example:** `/api/users` - go here to get user data; `/api/orders` - go here to get order data.

### Entity
**Plain English:** A thing in your system with an identity that persists over time. You're the same "you" even after you change your hair color.

**Example:** A User is an entity - they keep the same ID even when they update their email.

### Environment Variables
**Plain English:** Secret settings stored outside your code. Like keeping your house key under a rock instead of in your pocket.

**Example:** `DATABASE_URL` tells your app where to find the database, but it's not written in the code anyone can read.

---

## F

### Fallback
**Plain English:** A backup plan when the main approach fails. Like having a spare tire.

**Example:** If the AI service is down, show a pre-written helpful message instead of an error.

### Frontend
**Plain English:** The parts of the program users see and interact with - the dining room of a restaurant. Buttons, forms, displays.

**Example:** The login page, the dashboard, the chat interface.

---

## G

### Git
**Plain English:** A system that tracks every change to your code. Like "Track Changes" in Word, but much more powerful.

**Key concepts:**
- **Commit:** Saving a snapshot of your changes
- **Push:** Uploading your commits to the cloud
- **Pull:** Downloading others' commits

### Guardrail
**Plain English:** A rule that prevents AI from doing something unwanted. Like a bumper in bowling.

**Example:** "Never give medical advice" - if a user asks about medication, redirect to see a doctor.

---

## H

### Hook
**Plain English:** A way to "hook into" something happening and run your code. Like a doorbell that triggers a camera.

**Example:** In React, `useState` is a hook that lets components remember values.

---

## I

### Integration
**Plain English:** Connecting two systems so they work together. Like an adapter that lets your European plug work in American outlets.

**Example:** Connecting your app to Stripe so users can pay.

---

## J

### JSON (JavaScript Object Notation)
**Plain English:** A format for organizing data that both humans and computers can read. Like a structured form.

```json
{
  "name": "Marcus",
  "email": "marcus@example.com",
  "age": 32
}
```

---

## L

### LLM (Large Language Model)
**Plain English:** The AI brain behind ChatGPT, Claude, etc. Trained on massive text data to understand and generate language.

**Example:** Claude is an LLM made by Anthropic.

### Latency
**Plain English:** The delay between asking for something and getting it. Like wait time at a restaurant.

**Example:** "Response latency is 200ms" means it takes 0.2 seconds to get an answer.

---

## M

### Migration
**Plain English:** Changing your database structure in a controlled way. Like remodeling a house while people still live there.

**Example:** Adding a "phone_number" column to your users table.

### Monolith
**Plain English:** All your code in one big program. Like a house where everything is under one roof.

**Opposite:** Microservices - separate small programs that talk to each other.

### Multi-tenancy
**Plain English:** One system serving multiple separate customers. Like an apartment building - one building, many tenants, each with their own private space.

**Example:** Slack - one app, thousands of companies, each sees only their own data.

---

## P

### P95/P99
**Plain English:** Performance measurements for "almost everyone." P95 means 95% of requests are faster than this time.

**Example:** "P95 latency is 500ms" means 95% of users get a response in under half a second.

### Payload
**Plain English:** The data being sent in a request. Like the contents of an envelope.

**Example:** When you submit a form, the payload is all the form fields.

### Production
**Plain English:** The real, live system that actual users use. Like opening night of a play.

**Opposite:** Staging (dress rehearsal) or Development (practice).

### Prompt
**Plain English:** Instructions given to an AI to get a specific response. Like a question you ask.

**Example:** "You are a productivity coach. The user says: 'I'm feeling tired.' Respond encouragingly."

---

## R

### RAG (Retrieval-Augmented Generation)
**Plain English:** Giving an AI access to external documents so it can answer questions about them. Like an open-book test.

**Example:** Uploading your company handbook so the AI can answer policy questions.

### Rollback
**Plain English:** Undoing a deployment and going back to the previous version. Like pressing "undo" after making a mistake.

**Example:** New code broke the checkout - rollback to yesterday's version while we fix it.

---

## S

### Schema
**Plain English:** The structure/blueprint of your data. Like a template form showing what fields exist.

**Example:** User schema: id, email, name, created_at

### Staging
**Plain English:** A copy of your production system for testing. Like a dress rehearsal before opening night.

**Example:** Test the new feature on staging first, then deploy to production.

### State
**Plain English:** The current condition of something that can change. Like whether a light switch is on or off.

**Example:** An order's state: pending → paid → shipped → delivered

### State Machine
**Plain English:** Rules about what states something can be in and how it moves between them. Like a flow chart.

**Example:** An order can go from "pending" to "paid" but not directly from "pending" to "delivered."

---

## T

### TDD (Test-Driven Development)
**Plain English:** Writing tests BEFORE writing code. Like making a checklist before starting a project.

1. Write a test (it fails - RED)
2. Write code to pass the test (GREEN)
3. Clean up the code (REFACTOR)
4. Repeat

### Token
**Plain English:** A small piece of text that AI models process. Roughly 4 characters = 1 token.

**Why it matters:** AI services charge per token, and there's a limit on how many tokens fit in the context window.

### TypeScript
**Plain English:** JavaScript with added safety checks. Like spell-check for code - catches mistakes before you run it.

---

## U

### Ubiquitous Language
**Plain English:** The agreed-upon vocabulary for your project. Everyone uses the exact same words for the same things.

**Example:** Always say "Intention" - never "goal," "task," or "todo."

---

## V

### Validation
**Plain English:** Checking if data is acceptable before using it. Like a bouncer checking IDs.

**Example:** Checking that an email has an @ sign before saving it.

---

## W

### Webhook
**Plain English:** A notification sent from one service to another when something happens. Like a text message saying "your package was delivered."

**Example:** Stripe sends a webhook to your app when a payment succeeds.
