# 🇮🇳 India Locations JSON Data

[![JSON Data](https://img.shields.io/badge/Data-JSON-blue.svg)](#)
[![Locations](https://img.shields.io/badge/Locations-600k%2B-success.svg)](#)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](#)

A comprehensive, hierarchical JSON dataset of geographical and administrative divisions across India. This dataset is perfect for populating cascading dropdown menus, geographic databases, and location-based filtering.

---

## 📑 Table of Contents

- [Overview](#-overview)
- [Data Structure](#-data-structure)
- [Use Cases](#-use-cases)
- [Generation Script](#-generation-script)
- [Acknowledgements](#-acknowledgements)
- [License](#-license)

---

## 📖 Overview

This repository contains `india_locations.json`, a highly detailed list of all locations in India, encompassing:
- **36** States and Union Territories
- **700+** Districts
- **600,000+** Cities, Towns, and Villages

The data is flattened and alphabetically sorted for easy integration into front-end components and back-end databases.

## 🏗 Data Structure

The JSON is formatted as an array of state objects. Each state object contains an array of its constituent districts, and each district contains a sorted array of strings representing all cities, towns, and villages within it.

```json
[
  {
    "state": "State Name",
    "districts": [
      {
        "district": "District Name",
        "cities": [
          "City/Village 1",
          "City/Village 2",
          "..."
        ]
      }
    ]
  }
]
```

## 🚀 Use Cases

- **Cascading Dropdowns:** Build seamless `State → District → City/Village` selection forms.
- **Geographical Mapping:** Power location-based search and filtering features.
- **Data Seeding:** Populate your SQL or NoSQL database with exhaustive Indian location records.

## ⚙️ Generation Script

Included is `fetch_cities.js`, a Node.js script used to generate this dataset. 

It works by:
1. Downloading raw, highly-nested location data.
2. Parsing and extracting sub-districts.
3. Flattening everything into a single `cities` array for each district.
4. Sorting entries alphabetically to ensure a clean UX for dropdowns.

**Usage:**
```bash
node fetch_cities.js
```

## 🙏 Acknowledgements

This dataset is aggregated and flattened from a comprehensive data collection originally sourced from [villageinfo.in](https://villageinfo.in/) and structured by the amazing open-source community, specifically [pranshumaheshwari/indian-cities-and-villages](https://github.com/pranshumaheshwari/indian-cities-and-villages).

## 📄 License

This project is open-source and available under the MIT License.
