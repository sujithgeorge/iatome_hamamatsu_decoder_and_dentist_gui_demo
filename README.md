# ALERIO clinic demo

A single-page demo of a dentist chairside workspace and the Hamamatsu flat-panel decoding pipeline. It runs entirely in the browser. There is no build step and no server-side app.

## Run

```bash
python3 -m http.server 8765
```

Open http://127.0.0.1:8765/

Sample frames and dentist photos are loaded from S3, so serve the folder over HTTP instead of opening `index.html` as a file.

## Dentist workspace

Select a dentist to open the shared clinic list. There is no login.

Patients, visits, notes, prescriptions, and X-ray images are stored in IndexedDB in this browser. Creating a patient assigns an ID and sets the first-visit date to today.

**Take X-ray** uses the built-in sample radiograph, not a live sensor. The scan is saved to the visit as soon as it is captured. Notes and the medicine prescription are saved only when you click **Save visit details**. Leaving a visit with unsaved notes or a prescription asks you to confirm.

## Hamamatsu decoding pipeline

The pipeline applies dark subtraction, then shading (flat-field) correction. It needs four 1000×1506 little-endian uint16 frames, each with a 16-byte prefix (3,012,016 bytes):

| Frame | Role |
| --- | --- |
| Idr | Dark frame for the open-beam reference |
| Ido | Dark frame for the object exposure |
| Ixr | Open-beam X-ray reference |
| Ixo | Object X-ray exposure |

Choose **Use sample data**, or **Upload my files** and supply all four. **Process Frames and View Result** shows the corrected radiograph and the intermediate stages. **Explain the algorithm** describes the correction steps.

## Layout

The demo is one file: `index.html`.
