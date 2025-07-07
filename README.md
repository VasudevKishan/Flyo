# Fylo

A mini project built with Tailwind CSS, bundled using Webpack, and deployed to Netlify via GitHub Actions.

[![Production Site](https://img.shields.io/badge/Live%20Demo-Netlify-green?logo=netlify)](https://vasudev-flyo.netlify.app/)

[View the production site on Netlify &rarr;](https://vasudev-flyo.netlify.app/)

---

## Project Structure

- **`index.html`**: Main HTML file.
- **`script.js`**: Main JavaScript entry point (imports styles and handles theme toggling).
- **`input.css`**: Tailwind CSS source file (contains Tailwind directives and custom styles).
- **`css/style.css`**: Generated CSS file from Tailwind CLI.
- **`images/`**: Contains all image assets.
- **`webpack.config.js`**: Webpack configuration.
- **`.github/workflows/deploy.yaml`**: GitHub Actions workflow for deployment.

---

## Webpack Setup

This project uses [Webpack](https://webpack.js.org/) for bundling JavaScript and CSS assets:

- **Entry Point**: `script.js` is the main entry file.
- **CSS Handling**: Tailwind CSS is processed via the CLI (`input.css` → `css/style.css`). The generated CSS is imported in `script.js` and bundled by Webpack using `style-loader` and `css-loader`.
- **Image Assets**: All images in the `images/` folder are copied to the `dist/images/` directory using `copy-webpack-plugin`. Images imported in JS/CSS are also emitted to `dist/images/` via Webpack's asset modules.
- **Output**: The final build is output to the `dist/` directory, with all assets properly organized.

**Key Webpack Features:**

- Babel is used for JS transpilation.
- HTML is generated from `index.html` using `html-webpack-plugin`.
- The dev server runs on port 3000 with hot reloading.

---

## Deployment: Netlify via GitHub Actions

Deployment is automated using GitHub Actions and Netlify:

- **Workflow File**: See `.github/workflows/deploy.yaml`.
- **Trigger**: On every push to the `master` branch.
- **Steps**:
  1. **Checkout** the repository code.
  2. **Setup Node.js** (version 18).
  3. **Install dependencies** using `npm install`.
  4. **Build the project** using `npm run build` (runs Webpack and Tailwind build scripts).
  5. **Deploy to Netlify** using the [nwtgck/actions-netlify](https://github.com/nwtgck/actions-netlify) GitHub Action, publishing the contents of the `dist/` directory.

**Secrets Required:**

- `NETLIFY_AUTH_TOKEN`
- `NETLIFY_SITE_ID`
- `GITHUB_TOKEN` (provided by GitHub Actions)

---

## Development

To run locally:

```sh
npm install
npm run build:css   # Build Tailwind CSS
npm run watch        # Watch Tailwind CSS for changes
npm run dev         # Start Webpack dev server
```

To build for production:

```sh
npm run build:css
npm run build
```

---

## License

MIT
