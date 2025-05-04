# Codex Demo Form

A demonstration of a contact information form built using Wikimedia Design Codex components. This project shows how to implement a form that collects first name, last name, email address, phone number, and description using Codex design system.

## Overview

This project uses Codex, the Wikimedia Design System, to build a user interface with a consistent, accessible, and translatable design. The form includes validation, error states, and responsive layout.

## Features

- Form fields for first name, last name, email, phone, and description
- Validation for required fields and format validation for email and phone
- Success message on submission
- Reset functionality
- Accessible design using Codex components

## Technologies Used

- Vue.js 3 (Composition API)
- Wikimedia Design Codex Components:
  - CdxField - For form field containers with labels and help text
  - CdxTextInput - For text inputs (first name, last name, email, phone)
  - CdxTextArea - For the description field
  - CdxButton - For Submit and Reset buttons
  - CdxMessage - For the success message
- Vite for building and development

## Components Used

The form uses the following Codex components:

1. **CdxField**: Container component for form fields that provides label, description, and help text.
2. **CdxTextInput**: Input component for single-line text entry.
3. **CdxTextArea**: Text area component for multi-line text entry.
4. **CdxButton**: Button component for form actions.
5. **CdxMessage**: Message component for displaying success feedback.

## Getting Started

### Prerequisites

- Node.js (v14 or higher recommended)
- npm (v7 or higher)

### Installation

1. Clone the repository:
```bash
git clone https://github.com/baba786/codex-demo-form.git
cd codex-demo-form
```

2. Install dependencies:
```bash
npm install
```

3. Start the development server:
```bash
npm run dev
```

4. Open your browser to `http://localhost:3000`

## Project Structure

```
codex-demo-form/
├── public/               # Static assets
├── src/
│   ├── App.vue           # Main application component with form
│   └── main.js           # Application entry point
├── index.html            # HTML entry point
├── package.json          # Project dependencies and scripts
├── vite.config.js        # Vite configuration
└── README.md             # Project documentation
```

## Form Validation

The form includes the following validation:

- First Name: Required field
- Last Name: Required field
- Email: Required field with email format validation
- Phone: Optional field with format validation
- Description: Optional field

## Additional Resources

- [Codex Documentation](https://doc.wikimedia.org/codex/latest/)
- [Vue.js Documentation](https://vuejs.org/guide/introduction.html)
- [Wikimedia Design Style Guide](https://design.wikimedia.org/style-guide/)

## License

This project is available under the MIT License.
