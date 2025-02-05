<img src="./assets/web-ui.png" alt="Browser Use Web UI" width="full"/>

This project builds upon the foundation of the [browser-use](https://github.com/browser-use/browser-use), which is designed to make websites accessible for AI agents.

**WebUI:** This interface is powered by Gradio and offers many of the functionalities you'd find in typical browser usage. It's designed for ease of use, making it straightforward for users to interact with the browser agent.

**Expanded LLM Support:** Our platform now includes compatibility with a range of Large Language Models (LLMs), such as Gemini, OpenAI, Azure OpenAI, Anthropic, DeepSeek, Ollama, and more. We're committed to expanding this list to include additional models in the future.

**Custom Browser Support:** Users have the option to operate their own browser within our tool. This eliminates the hassle of repeated logins and other authentication issues and includes support for high-definition screen recording.

**Persistent Browser Sessions:** Users have the option to maintain their browser session open across different AI tasks. This allows for continuity, enabling users to view a complete history and the current state of AI interactions.

<video src="https://github.com/user-attachments/assets/56bc7080-f2e3-4367-af22-6bf2245ff6cb" controls="controls">Your browser does not support playing this video!</video>

## Installation Guide

### Prerequisites

- Python 3.11 or higher
- Git (for cloning the repository)

### Option 1: Local Installation

Read the [quickstart guide](https://docs.browser-use.com/quickstart#prepare-the-environment) or follow the steps below to get started.

#### Step 1: Clone the Repository

```bash
git clone https://github.com/browser-use/web-ui.git
cd web-ui
```

#### Step 2: Set Up Python Environment

We recommend using [uv](https://docs.astral.sh/uv/) for managing the Python environment.

Using uv (recommended):

```bash
uv venv --python 3.11
```

Activate the virtual environment:

- Windows (Command Prompt):

```cmd
.venv\Scripts\activate
```

- Windows (PowerShell):

```powershell
.\.venv\Scripts\Activate.ps1
```

- macOS/Linux:

```bash
source .venv/bin/activate
```

#### Step 3: Install Dependencies

Install Python packages:

```bash
uv pip install -r requirements.txt
```

Install Playwright:

```bash
playwright install
```

#### Step 4: Configure Environment

1. Create a copy of the example environment file:

- Windows (Command Prompt):

```bash
copy .env.example .env
```

- macOS/Linux/Windows (PowerShell):

```bash
cp .env.example .env
```

2. Open `.env` in your preferred text editor and add your API keys and other settings

### Option 2: Docker Installation

#### Prerequisites

- Docker and Docker Compose installed
  - [Docker Desktop](https://www.docker.com/products/docker-desktop/) (For Windows/macOS)
  - [Docker Engine](https://docs.docker.com/engine/install/) and [Docker Compose](https://docs.docker.com/compose/install/) (For Linux)

#### Installation Steps

1. Clone the repository:

```bash
git clone https://github.com/browser-use/web-ui.git
cd web-ui
```

2. Create and configure environment file:

- Windows (Command Prompt):

```bash
copy .env.example .env
```

- macOS/Linux/Windows (PowerShell):

```bash
cp .env.example .env
```

Edit `.env` with your preferred text editor and add your API keys

3. Run with Docker:

```bash
# Build and start the container with default settings (browser closes after AI tasks)
docker compose up --build
```

```bash
# Or run with persistent browser (browser stays open between AI tasks)
CHROME_PERSISTENT_SESSION=true docker compose up --build
```

4. Access the Application:

- Web Interface: Open `http://localhost:7788` in your browser
- VNC Viewer (for watching browser interactions): Open `http://localhost:6080/vnc.html`
  - Default VNC password: "youvncpassword"
  - Can be changed by setting `VNC_PASSWORD` in your `.env` file

## Usage

### Local Setup

1. **Run the WebUI:**
   After completing the installation steps above, start the application:

   ```bash
   python webui.py --ip 127.0.0.1 --port 7788
   ```
2. WebUI options:

   - `--ip`: The IP address to bind the WebUI to. Default is `127.0.0.1`.
   - `--port`: The port to bind the WebUI to. Default is `7788`.
   - `--theme`: The theme for the user interface. Default is `Ocean`.
     - **Default**: The standard theme with a balanced design.
     - **Soft**: A gentle, muted color scheme for a relaxed viewing experience.
     - **Monochrome**: A grayscale theme with minimal color for simplicity and focus.
     - **Glass**: A sleek, semi-transparent design for a modern appearance.
     - **Origin**: A classic, retro-inspired theme for a nostalgic feel.
     - **Citrus**: A vibrant, citrus-inspired palette with bright and fresh colors.
     - **Ocean** (default): A blue, ocean-inspired theme providing a calming effect.
   - `--dark-mode`: Enables dark mode for the user interface.
3. **Access the WebUI:** Open your web browser and navigate to `http://127.0.0.1:7788`.
4. **Using Your Own Browser(Optional):**

   - Set `CHROME_PATH` to the executable path of your browser and `CHROME_USER_DATA` to the user data directory of your browser. Leave `CHROME_USER_DATA` empty if you want to use local user data.
     - Windows

       ```env
        CHROME_PATH="C:\Program Files\Google\Chrome\Application\chrome.exe"
        CHROME_USER_DATA="C:\Users\YourUsername\AppData\Local\Google\Chrome\User Data"
       ```

       > Note: Replace `YourUsername` with your actual Windows username for Windows systems.
       >
     - Mac

       ```env
        CHROME_PATH="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"
        CHROME_USER_DATA="/Users/YourUsername/Library/Application Support/Google/Chrome"
       ```
   - Close all Chrome windows
   - Open the WebUI in a non-Chrome browser, such as Firefox or Edge. This is important because the persistent browser context will use the Chrome data when running the agent.
   - Check the "Use Own Browser" option within the Browser Settings.
5. **Keep Browser Open(Optional):**

   - Set `CHROME_PERSISTENT_SESSION=true` in the `.env` file.

### Docker Setup

1. **Environment Variables:**

   - All configuration is done through the `.env` file
   - Available environment variables:

     ```
     # LLM API Keys
     OPENAI_API_KEY=your_key_here
     ANTHROPIC_API_KEY=your_key_here
     GOOGLE_API_KEY=your_key_here

     # Browser Settings
     CHROME_PERSISTENT_SESSION=true   # Set to true to keep browser open between AI tasks
     RESOLUTION=1920x1080x24         # Custom resolution format: WIDTHxHEIGHTxDEPTH
     RESOLUTION_WIDTH=1920           # Custom width in pixels
     RESOLUTION_HEIGHT=1080          # Custom height in pixels

     # VNC Settings
     VNC_PASSWORD=your_vnc_password  # Optional, defaults to "vncpassword"
     ```
2. **Browser Persistence Modes:**

   - **Default Mode (CHROME_PERSISTENT_SESSION=false):**

     - Browser opens and closes with each AI task
     - Clean state for each interaction
     - Lower resource usage
   - **Persistent Mode (CHROME_PERSISTENT_SESSION=true):**

     - Browser stays open between AI tasks
     - Maintains history and state
     - Allows viewing previous AI interactions
     - Set in `.env` file or via environment variable when starting container
3. **Viewing Browser Interactions:**

   - Access the noVNC viewer at `http://localhost:6080/vnc.html`
   - Enter the VNC password (default: "vncpassword" or what you set in VNC_PASSWORD)
   - You can now see all browser interactions in real-time
4. **Container Management:**

   ```bash
   # Start with persistent browser
   CHROME_PERSISTENT_SESSION=true docker compose up -d

   # Start with default mode (browser closes after tasks)
   docker compose up -d

   # View logs
   docker compose logs -f

   # Stop the container
   docker compose down
   ```


## Developer Information

- **LinkedIn**: [Ahsan Saeed](https://www.linkedin.com/in/ahsensaeed/)
- **Hugging Face**: [ahsansaeed](https://huggingface.co/ahsansaeed)
- **LeetCode**: [AhsanSaeed](https://leetcode.com/u/AhsanSaeed/)
