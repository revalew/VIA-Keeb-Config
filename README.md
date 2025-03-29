# Keychron Q8 ANSI Knob

<br/><br/>

My setup is based on the [Keychron Q8 ANSI Knob](https://www.keychron.com/products/keychron-q8-alice-layout-qmk-custom-mechanical-keyboard) keyboard.

<br/><br/>

## Updating the keyboard firmware

<br/>

**I used the Windows 11 VM (where I installed the QMK toolbox and the required drivers), and Edge browser to configure the keeb (as specified in the instructions below).**

<br/>

To update the firmware follow the instructions:

1. [Keychron website](https://www.keychron.com/pages/how-to-factory-reset-or-use-the-launcher-web-app-to-flash-firmware-for-your-keyboard),

2. [`Keychron_Use_Web_App_to_Flash_Firmware.pdf`](./Keychron_Use_Web_App_to_Flash_Firmware.pdf) file in the same directory as this document.

<br/><br/>

## Update the layout

<br/>

After the update I used the [Linux AppImage version of VIA](https://github.com/the-via/releases/releases/download/v3.0.0/via-3.0.0-linux.AppImage)
to configure the layout and saved it in the same directory as this file in JSON format - [available here](./keychron_q8_ansi_knob.layout.json).

<br/><br/>

## Print to PDF

<br/>

Use custom page size and remove the page breaks when using `Print to PDF` (`JS` injection using the `DevTools` to save the [instructions](./Keychron_Use_Web_App_to_Flash_Firmware.pdf) locally)

<br/>

```js
// INJECT THIS THROUGH THE CONSOLE
// TO REMOVE THE PAGE-BREAKS
function setPageSize(width = "21cm", height = "400cm") {
  console.log("Fetching page size from user...")

  // 21cm = A4 width, height 400cm
  // width = prompt("Specify the width of the PDF page (e.g. 21cm):", "21cm");

  height = prompt("Specify the height of the PDF page (e.g. 400cm):", "400cm");



  console.log("Checking if styles exist...")

  let existingStyle = document.getElementById("dynamic-print-style");
  if (existingStyle) {

    console.log("Previous styles deleted...")

    existingStyle.remove(); // Delete previous styles if they exist
  }

  console.log("Creating new styles...")

  let styleTag = document.createElement("style");
  styleTag.id = "dynamic-print-style"; // Set ID to enable overwriting

  styleTag.textContent = `@media print {
  @page { size: ${width} ${height}; margin: 0; padding: 0; }

  html, body {
    width: ${width};
    height: auto;
    overflow: visible;
    /* Uncomment if you want black PDF */
    /* background-color: #121212 !important; */
    /* color: #ffffff !important; */
  }

  body {
    transform: scale(1);
    transform-origin: top left;
  }

  * {
    page-break-before: avoid !important;
    page-break-after: avoid !important;
    page-break-inside: avoid !important;
  }
}`;
  document.head.appendChild(styleTag);

  // Screw them "!important" styles on print
  // Use as needed
  // document.querySelectorAll("table, th, td").forEach(el => {
    // el.style.setProperty("background-color", "#121212", "important");
    // el.style.setProperty("color", "#ffffff", "important");
  // });
};

setPageSize()
```

<br/><br/>
