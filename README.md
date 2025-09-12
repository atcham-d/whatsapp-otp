WhatsApp OTP Verification Landing Page
This project is a simple, static web application that provides a front-end for a user registration flow using WhatsApp for One-Time Password (OTP) verification. The backend logic is handled entirely by N8N workflows, which integrate with Supabase for data storage and the Meta Business API for sending messages.

Project Architecture
This project is decoupled into a static front-end and a low-code backend, making it scalable and easy to manage.

Front-end: A clean, interactive index.html file with vanilla JavaScript and CSS. It captures user input and communicates with the N8N backend.

Backend Workflow: Two separate N8N workflows handle all the business logic:

Send OTP Workflow: Generates an OTP, saves a hashed version to the database, and sends the plain OTP to the user's WhatsApp.

Verify OTP Workflow: Receives the user's OTP, validates it against the database record, and updates the user's status.

Database: A Supabase PostgreSQL database is used to store user registration information, including their status (pending_verification, registered, paid, etc.).

How It Works (User Flow)
Step 1: Registration

A user enters their username and WhatsApp number on the index.html page.

The front-end sends a POST request to the "Send OTP" N8N workflow.

N8N creates a new user record in Supabase with the status pending_verification and sends a 6-digit OTP to the user's WhatsApp.

Step 2: Verification

The user enters the received OTP on the webpage.

The front-end sends a POST request to the "Verify OTP" N8N workflow.

N8N finds the user's record, checks if the OTP is correct and not expired, and updates the user's status to registered.

Step 3: Next Steps (e.g., Payment)

Once a user is verified, further workflows can be triggered to handle subsequent actions like processing payments and adding credits, as outlined in the original plan.

Project Setup
To get this project running, you need to configure the front-end and set up the backend workflows.

Prerequisites
A Supabase account with a registrations table created.

An N8N account (Cloud or self-hosted).

A Meta Business account with a configured WhatsApp application.

1. Configure the Front-end
The index.html file is the only front-end file you need. Open it and find the following JavaScript variables:

const sendOtpUrl = 'PASTE_YOUR_N8N_SEND_OTP_URL_HERE';
const verifyOtpUrl = 'PASTE_YOUR_N8N_VERIFY_OTP_URL_HERE';

Replace the placeholder URLs with the Production URLs from your two N8N webhook nodes.

2. Build the N8N Workflows
Log in to your N8N account and build the two workflows (Send OTP and Verify OTP) as planned.

Make sure to add your Supabase and WhatsApp credentials to N8N.

Activate both workflows to enable their Production URLs.

3. Running the Project
There is no server to run for this project. Simply open the index.html file in your web browser.

The page is fully self-contained and will communicate with your live N8N workflows.