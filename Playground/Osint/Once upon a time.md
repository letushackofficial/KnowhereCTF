# Once Upon a Time: OSINT Writeup

| | |
|---|---|
| **Challenge** | Once Upon a Time |
| **Category** | OSINT / Geolocation |
| **Flag** | `LUH{infosys-bengaluru-terminal-building_50-2008}` |

---

## Table of Contents

1. [Challenge Description](#1-challenge-description)
2. [Initial Analysis](#2-initial-analysis)
3. [Decoding the Description](#3-decoding-the-description)
4. [Dead End: Reverse Image Search](#4-dead-end-reverse-image-search)
5. [The UFO Angle](#5-the-ufo-angle)
6. [Breakthrough: The Pyramid](#6-breakthrough-the-pyramid)
7. [Confirming the Location](#7-confirming-the-location)
8. [Getting the Flag](#8-getting-the-flag)
9. [Summary](#9-summary)

---

## 1. Challenge Description

> The UFO that came to earth mistook this for something else.

**Flag format:**

```
luh{Location-city-name of the building pic1-name of building pic2-year of the photo taken}
```

**Note:** `luh{all_small_letters}` and replace spaces with `_`.

The challenge shipped with a zip file containing two images.

---

## 2. Initial Analysis

### Metadata

Neither image has any metadata, so EXIF is a dead end. This looks like a **geolocation-style OSINT** challenge: the answer has to come from what is visible in the pictures.

### Image 1

![Image 1](https://github.com/user-attachments/assets/29a019d5-a9cc-4976-b40d-ad1571656959)

Observations:

- The structure looks **still under construction**
- There is a **gap in the roof**
- The walls appear to be **lined with glass panels**
- There is an **obstruction** in view. Could it be a pole?

### Image 2

![Image 2](https://github.com/user-attachments/assets/1dbaaf8a-07a5-44c4-abd3-9c488990d605)

This image is very blurry, but a few details stand out:

- A **unique structure in the middle**, possibly a support
- It looks like a **circular support for a circular building**
- **Black objects** sit right beside the support. Possibly chairs?

### Are these the same place?

Both images seem to come from the same place, but they may show different buildings. One looks like it is under construction, while the other has a polished interior.

---

## 3. Decoding the Description

The description is oddly worded, so it is probably a hint:

- What does it mean that the UFO *mistook it for something else*?
- What is the "it" being mistaken?
- The flag asks for a **year**, and the challenge is called *"Once Upon a Time"*, so the photos are most likely **not recent**.

---

## 4. Dead End: Reverse Image Search

Reverse image search only added confusion. There are **many buildings with the same roof structure**, so there was no clear match.

---

## 5. The UFO Angle

Since the images alone were not giving much, the focus shifted to the UFO theme:

- Why does the description mention a UFO at all? Is it just the CTF theme?
- Even so, what would a UFO be searching for, and what could it mistake for something else?

Searching around **UFO theories** led to a new lead.

---

## 6. Breakthrough: The Pyramid

![Pyramid lead](https://github.com/user-attachments/assets/f17cc3cc-20c4-4202-a637-8f069ff79372)

The UFO research suggested a **pyramid**. Based on the buildings in the images, a pyramid nearby seemed unlikely, but it did not hurt to search for one.

The search turned up a pyramid-shaped building:

![Pyramid result](https://github.com/user-attachments/assets/ac8121a0-2e18-4dce-aa39-5fedc1437036)

> That one there seems to have the same shape as seen in the images.

It appeared to be located at **Infosys**.

---

## 7. Confirming the Location

Next step was to verify it on **Google Maps**.

![Google Maps check 1](https://github.com/user-attachments/assets/d78370c6-58f9-4876-9254-cf9fb8121783)

![Google Maps check 2](https://github.com/user-attachments/assets/5ba74ec3-72c5-4995-b129-12794126ccaa)

Findings:

- The second building matched what was seen in the challenge images
- The **pole** seen as an obstruction in the image appears to belong to this building

This confirmed the location as an **Infosys campus in Bengaluru**, with the building being a **terminal building**.

---

## 8. Getting the Flag

With the location, city and building name identified, the remaining unknown was the **building number**. The template was tried with the year **2008**, so only the number needed to be brute-forced:

```
LUH{infosys-bengaluru-terminal-building_xx-2008}
```

The correct value was **50**, and the flag was accepted:

```
LUH{infosys-bengaluru-terminal-building_50-2008}
```

---

## 9. Summary

| Step | Finding |
|---|---|
| Metadata | None available |
| Visual clues | Glass-panelled walls, roof gap, circular central support, possible pole |
| Reverse image search | Inconclusive, many look-alike roofs |
| Description hint | UFO theory led to the pyramid idea |
| Location | Infosys, Bengaluru |
| Building | Terminal building, number 50 |
| Year | 2008 |

### Takeaways

- When image metadata is stripped, lean on **architectural details**.
- Odd challenge wording is often a **hint**. The UFO angle led to the pyramid-shaped building.
- Reverse image search can fail on generic structures, so combine it with **thematic and contextual research**.
- Confirm candidates on **Google Maps** before committing.

---

*Flag: `LUH{infosys-bengaluru-terminal-building_50-2008}`*
