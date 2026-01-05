# Hyperhidrosis Survey Platform

## Purpose

This repository contains code and documentation for building a modular survey system dedicated to collecting comprehensive, anonymized data about hyperhidrosis experiences across different treatments, severities, climates, and demographics. The goal is to provide a transparent and community‑driven dataset that can be shared publicly to help sufferers and researchers understand treatment outcomes and lived experiences.

## Architecture Overview

The project follows a simple Model‑View‑Controller (MVC) inspired architecture:

- **View (Front‑End)**: Responsible for the presentation layer. This could be implemented as a series of web pages or forms hosted on WordPress or a static site. Each page handles a single segment of the survey, and after submission it redirects to the next segment. The view should not contain business logic beyond form validation and conditional navigation.

- **Intake (Controller & GPT)**: A custom GPT (public‑facing mode) acts as the intake assistant, guiding respondents through classification and clarifying questions before they complete the forms. It prepares the structured data payload for each segment. A second GPT (agent mode) will be used later for data curation and normalization; this repository includes a placeholder for those instructions.

- **Data Store (Model)**: All survey submissions are stored as events in AppSheet or another backend. Each event corresponds to a segment (e.g., baseline profile, treatment trial, outcomes) and includes a UUID linking back to the participant. This design allows for partial data and multiple sessions. The data store should remain technology‑agnostic—AppSheet or any other backend service can be used as long as it supports event‑level inserts.

## Custom GPT Instructions

### Public Intake Mode (Patient‑Facing)

The public‑facing GPT should:

- Explain hyperhidrosis types and treatments in plain language, inviting users to choose classifications and normalizing uncertainty.
- Avoid medical diagnoses, treatment recommendations, or dosing guidance.
- Maintain a calm, neutral, and respectful tone; avoid absolutes or alarmist language.
- Ask one question at a time and allow users to skip any question; explain why each question is being asked.
- Segment the conversation into independent modules (baseline profile, classification & onset, treatment trials, outcomes, follow‑up).
- For each completed module, output a JSON object containing `participant_uuid`, `segment_type`, `timestamp`, and only the fields explicitly discussed. Do not infer missing values.
- Emphasize that sensitive or potentially identifiable information is optional, and that all data will be anonymized for research.

### Agent Mode (Curator/Internal)

To be added. This mode will handle data normalization, contradiction detection, and curation logic without user interaction.

## Contributing

This project is open to collaborators. Please fork the repository and submit pull requests. All contributions should align with the modular design: update or add components in the appropriate layer without mixing concerns.

## Next Steps

- Finalize the public intake GPT instructions and integrate them into a custom GPT.
- Implement the front‑end forms with autosave and conditional navigation.
- Configure AppSheet tables for participants, baseline data, treatments, outcomes, and uploads.
- Test the minimum viable product with a single participant (Patient Zero) to validate flow and data capture.
