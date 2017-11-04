# Nuclear toi
### Table of Radioactive Isotopes (toi) API
An npm package to query data from the **Lund/LBNL Nuclear Data Search (http://nucleardata.nuclear.lu.se/toi/) Table of Isotopes**.
It queries data from the database and act as an API for their very simple (_and very, very yellow_) website. It behaves like an API for you, but what it actually does is making GET requests to their server and parsing the html tables they use.

At the moment this is very simple since it's born to serve a purpose in another program I'm working on for my master thesis, but I'm planning on actively expanding on it since the world deserves a better API to query nuclear data in Node.js.

## Features:
* Get all the possible elements decaying with gamma rays in a given energy
* Guess what elements may be responsible for a spectra by the energy peaks

## Usage examples:

* Get elements decaying with gamma rays from 300 keV to 301.999.. kEv
  ```javascript
  var Toi = require('nuclear-toi');

  // Everything returns a promise

  /**
   * Get the elements decaying at the specified energy range. return a promise
   * @param {number} from energy (integer)
   * @param {number} to energy (integer)
   */
  Toi.getGammaAtEnergyRange(300, 301).then(data => {
    for (var x of data) {
        console.log(x);
    }
  });
  ```
  Output:
  ```
  { Energy: 300, Intensity: 0.015, Element: '224Ac', Decay: 'a' }
  { Energy: 300, Intensity: 0.0225, Element: '223Fr', Decay: 'b-' }
  { Energy: 300, Intensity: 0.15, Element: '236Pa', Decay: 'b-' }
  { Energy: 300, Intensity: 0.23, Element: '151Dy', Decay: 'e+b+' }
  { Energy: 300, Intensity: 0.34, Element: '227Th', Decay: 'a' }
  { Energy: 300, Intensity: 2.32, Element: '227Th', Decay: 'a' }
  { Energy: 300, Intensity: 5.2, Element: '179Pt', Decay: 'e+b+' }
  { Energy: 300, Intensity: 6, Element: '134Sm', Decay: 'e+b+' }
  ....
  ```

* Get elements decaying at least with gamma energy 333±1 keV, 444±1 keV and 555±1 keV.
  ```javascript
  var Toi = require('nuclear-toi');
  /**
   * Get all the possible elements with the specified energies, within an error
   * @param {number[]} energyArray 
   * @param {number} error 
   */
   Toi.getPossibleElementsWithError([333,444,555], 1).then(data => {
      for (var x of data) {
          console.log(x);
      }
  });
  ```
  Output:
  ```
  185Au
  119I
  228Pa
  104mRh
  185Au
  ```

## Contact
For any question, new features request or problem please fill an issue or email me at dcat (at) protonmail (dot) com. I'll be glad to hear form you and try to help as I can.

This was made by Trintragula (Daniele) in 2017. Don't do this for anything evil and try to respect the service this is based on.

I'll write a blog post abou this sooner or later at [blog.danielescarinci.com](blog.danielescarinci.com)
