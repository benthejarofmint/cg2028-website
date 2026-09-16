# Elderly Fall Detection — Emergency Contact Page

A static web page shown when someone scans the NFC tag on a fall-detection
wearable (built on the STM32 B-L4S5I-IOT01A board). It gives a bystander
everything they need to help immediately: who the person is, relevant
medical information, and one-tap ways to call emergency services or the
person's next of kin.

This is a demo for a CG2028 lab project. All personal information on the
page (name, medical details, phone numbers, address) is fictional.

## Structure

- `index.html` — page content and structure
- `styles.css` — all styling

## Running locally

Open `index.html` directly in a browser, or serve the folder with any
static file server, e.g.:

```bash
python3 -m http.server 8000
```

Then visit `http://localhost:8000`.

## Deploying to GitHub Pages

1. Push this repository to GitHub.
2. In the repo settings, under **Pages**, set the source to the `main`
   branch, root folder.
3. GitHub will publish the page at
   `https://<username>.github.io/<repo-name>/`.
4. Point the NFC tag's stored URL at that address.
