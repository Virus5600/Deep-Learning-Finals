# Establishing Reproducible Evaluation Protocols for Resource-Constrained Deep Learning Training: A Systematic Framework with Educational Applications

This repository holds the codebase used in the research paper, holding three Jupyter Notebooks ([GPU](./src/gpu.ipynb) and [CPU](./src/cpu.ipynb) ~~and [Colab](./src/colab.ipynb)~~) that were used for the paper's experimentation.

<br>

## Contents

- [About the Repository](#empirical-analysis-of-early-stopping-and-learning-rate-scheduling-for-deep-learning-on-resource-constrained-hardware)
  - [Analytics](#analytics)
  - [Experiments](#experiments)
    - [GPU](#gpu)
    - [CPU](#cpu)
    - ~~[Colab](#colab)~~
   	  - [Notice](#colab-notice)
  - [How to Run](#how-to-run)
    - [Conda](#conda)
    - [Pip](#pip)
    - [Environment Keys](#environment-keys)
      - [`WEATHER_API`](#weather-api)
  - [License](#license)

<br>

## Analytics

The repository comes with the researcher's experiment logs. Analyzing these logs manually takes time and inefficient and thus, the [`analytics` Jupyter notebook](./src/analytics.ipynb) was added to make the analyzing process efficient and faster by reading the log files line-by-line before putting it in a dictionary which will then be converted into a dataframe, allowing the researcher to easily analyze it and even make graphs and plots while also allowing him to save it as a CSV or an Excel file.

## Experiments

Experiments were done in the following hardware specifications as per the study's Scope and Limitations.

- [GPU](#gpu)
- [CPU](#cpu)
- ~~[Colab](#colab)~~

---

### GPU

The GPU experimentation was done in a gaming laptop with **NVIDIA GeForce RTX 3050 Ti** with **4 GB of VRAM**, with **shared memory of 16 GB** from the system RAM.

The run is divided into 4 strategies, with 5 runs per strategy amounting to a total of 20 runs overall.

**NOTES:**

- Experimentation results can be seen in the [`out/gpu` directory](./out/gpu)
- Codebase is at [`src/gpu.ipynb`](./src/gpu.ipynb)

---

### CPU

For the CPU experimentation, it was done in a work-computer with **Intel i5-11400H** that has **32 GB of RAM**. GPU isn't utilize despite the fact that it is loaded with an **MVIDIA GeForce RTX 3050 Ti**.

Due to long training time per strategy, this platform was limited to a single run per strategy, resulting to a total of only 4 runs. (See Scope and Limitations of the paper).

**NOTES:**

- Experimentation results can be seen in the [`out/cpu` directory](./out/cpu)
- Codebase is at [`src/cpu.ipynb`](./src/cpu.ipynb)

---

### ~~Colab~~

~~Lastly, for the Colab experimentation, it uses the free-tier with [**resource limits**](https://research.google.com/colaboratory/faq.html#resource-limits), which falls into the research's scope.~~

~~**NOTES:**~~

- ~~Experimentation results can be seen in the [`out/colab` directory](./out/colab)~~
- ~~Codebase is at [`src/colab.ipynb`](./src/colab.ipynb)~~
  - ~~Code is the same as the GPU counterpart aside from all the `%pip install` in the first code block.~~

#### **COLAB NOTICE:**

Colab is dropped due to excessive limitations encountered during experimentation. Specifically, the volatility of GPU runtime availability in the free tier forced us onto a CPU-only session—an approach that, if continued, would have exceeded the project’s timeline.

---

## How to Run

As this environment uses Miniconda, `conda` users could simply run the code [below](#conda). However, as not everyone uses Anaconda or Miniconda, a `requirements.txt` is also provided within this repository to make sure others could still easily recreate the experiment by simply running the [`pip`](#pip) command.

The entire experiment (for CPU & GPU) are ran in Windows 11 OS with the GPU environment utilizing [NVIDIA CUDA](https://developer.nvidia.com/cuda-toolkit) as [required by Tensorflow](https://www.tensorflow.org/install/pip#windows-native). Furthermore, this experiment uses **Python 3.9** to utilize `tensorflow-gpu` in Windows Native as later versions requires an extensive setup that my time won't allow.

If you are a Linux user, you can probably use the later versions of Tensorflow and Python as seen in the [Tensorflow's Linux Installation guide](https://www.tensorflow.org/install/pip#linux). Just be sure to update all other packages if you wish too.

There are two separate environments since CPU uses the `tensorflow-cpu` which prevents the use of GPU if your device ever has one. The CPU environment also excludes CUDA and cuDNN, allowing the CPU environment to just utilize the CPU.

### Conda

For GPU environment:

```console
# In Conda's path
conda env create -f environment-gpu.yaml

# Relative path
conda env create -f environment-gpu.yaml --prefix=./.conda-gpu
```

For CPU environment:

```console
# In Conda's path
conda env create -f environment-cpu.yaml

# Relative path
conda env create -f environment-cpu.yaml --prefix=./.conda-cpu
```

This will install all necessary packages and the Python version used. And to use the environment, just use the `conda activate command`:

```console
# For GPU
conda activate .conda-gpu

# For CPU
conda activate .conda-cpu
```

In a case where the `pip`'s requirements aren't fully installed in the environment (due to the console not having elevated permissions), activate the said environment and use the respective `requirements` text file. See [next section](#pip) for more information.

### Pip

Before installing the requirements, make sure to use **Python 3.9**. You can check if it is using 3.9 by simply using the `python -V`.

For GPU environment:

```console
pip install -r requirements-gpu.txt
```

For CPU environment:

```console
pip install -r requirements-cpu.txt
```

Once ran, the command will install all the required dependencies.

### Environment Keys

At some point, the researcher decided to include API usage to automatically gather some data such as temperature of a location. This meant that various API keys are now optional as an environment key to utilize the said API.

#### Weather API

The experiment uses an API to get the environment of a location. It uses [WeatherAPI](https://www.weatherapi.com/), a free weather API endpoint with free tier, to get the temperature of a location.

For this experiment however, we just need to get the temperature so no codes needs to be modified. Just provide the API key in the `.env`'s `WEATHER_API` key to use the service and automatically set the temperature.

If the `WEATHER_API` key is blank or non-existent, it will default back to the provided `env_temp` value defined under the ***Mertrics related variables*** section.

On Google Colab experiment, the key is kept but not used as the cloud servers are in a controlled environment in which temperature is unknown.

## License

This repository is under [MIT License](./LICENSE) to allow students and researchers to use the source codes for their own experiments, research, and studies.
