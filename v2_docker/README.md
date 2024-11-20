# Pokémon Red Automation with Docker

This project uses Docker to set up an environment for running `baseline_fast_v2.py`, which automates gameplay for Pokémon Red. The setup is designed to take advantage of GPU acceleration, and results are stored on the host machine for easy retrieval.

## Requirements

- **Docker**:
  - Linux: Install [Docker Engine](https://docs.docker.com/engine/install/) and ensure GPU support is configured.
  - Windows: Use [Docker Desktop](https://www.docker.com/products/docker-desktop) with WSL2 integration enabled.
- A legally obtained `PokemonRed.gb` file placed in the working directory.

---

## Setup Instructions

1. **Configure the Scripts**:
   - Open `baseline_fast_v2.py` and set your desired variables according to your needs. I.e num_cpu = 64

2. **Build the Docker Container**:
   - Use the provided Dockerfile to build the container:
    
     docker build -t pokemon_red_automation .
    
2. **Run the Container**:
   - Create and Mount the `runs` directory to a volume for data storage:

     docker volume create runs_data
    
     docker run -d --gpus all -v runs_data:/app/runs pokemon_red_automation

     or

     docker compose up -d # Uses the compose file instead -d runs in background remove for interactive
    

---

## Known Issues

1. **No VNC Access**:  
   - Currently, the environment only runs in headless mode. GUI-based access (e.g., VNC) is not supported but may be added in the future.

2. **Deprecation Warning**:  
   - You may encounter the following warning during execution:  
    
     UserWarning: WARN: env.check_if_done to get variables from other wrappers is deprecated and will be removed in v1.0
    
   - This does not affect functionality but will be addressed in an upcoming update.

3. - GPU usage is only around 50% needs more testing.

---

## Notes

- The `runs` directory in the container is mounted to a volume on the host machine, making it easy to retrieve and store results.
- GPU acceleration is automatically handled in Windows via WSL2 and Docker Desktop. On Linux, ensure your system has GPU support set up and Docker is configured to use it.
- Image size is large at 10.47gb
- Important Legal Notice: The Pokémon Red ROM (PokemonRed.gb) is not included in the repository due to legal reasons. You must provide your own legally obtained ROM. The Docker image has not been pushed to the repository for similar legal considerations surrounding the distribution of ROM files.

---

## Future Improvements

- Addressing the `env.check_if_done` deprecation warning.
- Adding VNC or other GUI access for visual monitoring.
- Enhancing the script for better variable management and modularity.
- Reduce image size

---

Feel free to contribute or suggest improvements or point out issues on this! Thanks handofiron 😊
