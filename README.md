
# VisionControl Agent 🤖: AI-Powered Desktop GUI Automation

[![Python](https://img.shields.io/badge/Python-3.7+-blue.svg)](https://www.python.org/)
[![AI Agent](https://img.shields.io/badge/AI-Agent-brightgreen)](https://github.com/your-repo/VisionCraftAgent) <!-- Replace with actual repo link if available -->
[![Computer Vision](https://img.shields.io/badge/Computer%20Vision-YOLO%2FOCR-orange)](https://github.com/your-repo/VisionCraftAgent) <!-- Replace with actual repo link if available -->

VisionControl Agent is an innovative AI system that combines advanced computer vision with large language models to interact intelligently with desktop applications. It can:

👁️ See and understand graphical user interfaces in real-time

🧠 Interpret natural language commands with contextual awareness

🖱️ Act by controlling the GUI, performing tasks just like a human would

Whether it's automating workflows, testing applications, or enabling natural language control of software, VisionCraft bridges the gap between human intent and software execution.

## ✨ Features
🔧 Key Features
🗣️ Natural Language Control
    * Seamlessly control applications using simple English instructions.

👁️ Visual Interface Understanding
    * The system visually analyzes application GUIs using:

* YOLO for detecting UI elements like buttons and input fields

* OCR to extract visible text from those elements

* Seraphine to group related components for structured analysis

* Gemini Vision for high-level visual context and naming UI icons intelligently

🧠 LLM-Driven Task Execution
* Google's Gemini LLM interprets your commands and maps them to actionable GUI steps based on the visual interface.

🖱️ Automated GUI Interaction
* Executes mouse clicks and keyboard inputs using pyautogui with pixel-level precision.

🚀 Smart App Handling
* Launches and brings the target application (e.g., Windows Calculator) into focus using pygetwindow.

📸 Live Screenshot Analysis
* Continuously captures the application's screen to adapt decisions in real time.


## ⚙️ How It Works

The agent follows a sophisticated pipeline to achieve GUI automation:

1.  **Initialization:**
    *   The agent launches the target application (e.g., Windows Calculator) and brings it into focus.
    *   A screenshot of the application window is captured.
2.  **Computer Vision Analysis (`main.py`):**
    *   The screenshot is processed by the CV pipeline:
        *   **YOLO** detects potential UI elements and their bounding boxes.
        *   **OCR** reads text within these elements.
        *   **Seraphine** logically groups these elements.
        *   **Gemini Vision** analyzes the visual information, providing semantic names (e.g., `g_icon_name`) for elements.
    *   The output is a structured JSON containing identified UI elements with their properties (text, bounding box, `g_icon_name`).
3.  **User Command Input:**
    *   The user provides a natural language command (e.g., "Calculate 60 times 2 and then add 15 minus 9").
4.  **LLM Task Interpretation (`agent.py`):**
    *   The user's command and the list of recognized UI elements (specifically their `g_icon_name`s) are sent to a Gemini LLM.
    *   A carefully crafted system prompt guides the LLM to convert the command into a JSON array of `action_sequence` (e.g., `["6", "0", "multiply", "2", "equals", "add", "1", "5", "equals","minus", "9", "equals"]`).
5.  **Action Execution (`agent.py`):**
    *   The agent parses the `action_sequence` from the LLM's response.
    *   For each action (button label) in the sequence:
        *   It finds the corresponding UI element from the CV pipeline's output.
        *   It calculates the center coordinates of the element's bounding box relative to the application window.
        *   **`pyautogui`** is used to click on these coordinates, simulating user interaction.
6.  **Loop:** The agent can then await further commands or perform subsequent actions.

## 🛠️ Technologies Used

*   **Core Language:** Python 3.7+
*   **GUI Automation:** `pyautogui`
*   **Window Management:** `pygetwindow`
*   **Image Processing:** OpenCV, Pillow
*   **LLMs:** `google-genai` (for Gemini Pro and Gemini Vision Pro)
*   **CV Pipeline Components:**
    *   YOLO (Object Detection)
    *   OCR (e.g., Tesseract, or as part of a larger vision model)
    *   Seraphine (Custom Grouping Logic)
*   **Environment Management:** `python-dotenv`
*   **Utilities:** `subprocess`

## 🚀 Getting Started

### Prerequisites

*   Python 3.11 or higher.
*   Access to Google AI Studio and a `GEMINI_API_KEY`.
*   Windows Operating System (current implementation targets Windows Calculator, MacOS/Linux Support in development)

### Installation

1.  **Clone the repository (if applicable):**
    ```bash
    git clone <repository-url>
    cd ComputerAgent1
    ```
2.  **Create a virtual environment (recommended):**
    ```bash
    python -m venv venv
    venv\Scripts\activate  # Windows
    # source venv/bin/activate  # macOS/Linux
    ```
3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
4.  **Set up your environment variables:**
    *   Create a `.env` file in the `ComputerAgent1` directory.
    *   Add your Google API key to the `.env` file:
        ```
        GEMINI_API_KEY="YOUR_API_KEY_HERE"
        ```

### Running the Agent

1.  Ensure the target application (Windows Calculator) is available.
2.  Execute the main agent script:
    ```bash
    python agent.py
    ```
3.  The script will launch the Calculator, perform an initial visual analysis, and then prompt you to enter commands.

    Example command: `calculate 250 plus 400 then press equals`

## 🎯 Current Target Application

*   **Windows Calculator:** The agent is currently configured and demonstrated to work with the standard Windows Calculator application.

