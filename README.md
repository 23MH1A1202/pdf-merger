# Seamless PDF & Image Merger 📄🔄

A lightning-fast, fully client-side web application that allows users to easily combine multiple PDF documents and images into a single, neatly organized PDF file. 

Because all processing happens directly in the browser, your sensitive documents never touch a third-party server, ensuring **100% data privacy**.

---

## Access it using https://23mh1a1202.github.io/pdf-merger/

---

## ✨ Key Features

* **Complete Client-Side Processing:** Merging and rendering are handled entirely in your browser. No backend uploads means zero wait time and total privacy.
* **Smart Format Support:** Seamlessly combines both `.pdf` documents and image files (`.png`, `.jpg`, `.jpeg`).
* **Visual Reordering:** Features a highly intuitive, drag-and-drop grid interface. Easily click and drag document thumbnails to rearrange their sequence before merging.
* **Auto-Generated Previews:** Automatically generates visual thumbnail previews for the first page of uploaded PDFs and images.
* **Robust PDF Handling:** Includes an intelligent fallback mechanism. If a PDF has complex encodings, the app safely renders it as high-quality images and embeds them into the final document.
* **Interactive UI/UX:** Modern, responsive design with drag-and-drop upload zones, real-time progress overlays, and floating action buttons.

---

## 🛠 Tech Stack

Built as an efficient, lightweight single-page application (SPA) without the need for complex build tools or frameworks.

* **Frontend:** HTML5, CSS3 (Custom Variables & Grid), Vanilla JavaScript (ES6+)
* **PDF Generation & Manipulation:** [`pdf-lib`](https://pdf-lib.js.org/)
* **Document Parsing & Rendering:** [`pdf.js` (Mozilla)](https://mozilla.github.io/pdf.js/)
* **Drag-and-Drop Logic:** [`SortableJS`](https://sortablejs.github.io/Sortable/)

---

## 🚀 How to Run Locally

Because this is a zero-dependency, single-file application, running it is incredibly simple:

1. Clone or download the repository to your local machine.
2. Open the `index.html` file directly in any modern web browser (Chrome, Edge, Firefox, Safari).
3. *Alternatively:* Serve it using a simple local server like VS Code's "Live Server" extension for the best experience.

### Usage Instructions
1. **Upload:** Click the upload zone or drag and drop your PDFs and images into the dashed area.
2. **Reorder:** Click and hold any document card to drag it into your desired sequence.
3. **Remove:** Click the "X" button on any card to remove it from the queue.
4. **Merge:** Click the **"Combine Documents"** button.
5. **Download:** Once processing is complete, click **"Save PDF"** to download your merged file.

---

## 👨‍💻 Author

**Ambati Lalitha Sagar**
* Portfolio: [alsagar.tech](https://alsagar.tech)
* GitHub: [@23MH1A1202](https://github.com/23MH1A1202)
