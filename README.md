
# Fine-Tuning BERT on Linux Logs

This project fine-tunes a BERT model using PyTorch to classify Linux log messages. The BERT model is trained and evaluated on a dataset of structured Linux logs.

## Setup

1. **Clone the repository and navigate into the project directory:**\

   ```sh
   git clone https://github.com/gsampaio-rh/bert-linux-logs
   cd https://github.com/gsampaio-rh/bert-linux-logs
   ```

2. **Create a virtual environment and activate it:**

   ```sh
   python -m venv venv
   source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
   ```

3. **Install the required packages:**

   ```sh
   pip install pandas torch transformers scikit-learn
   pip install torch torchvision torchaudio
   ```

4. **Set the environment variable to enable MPS fallback (for macOS with MPS backend):**

   ```sh
   export PYTORCH_ENABLE_MPS_FALLBACK=1
   ```

## Usage

1. **Prepare the dataset:**
   Place your dataset CSV file in the project directory. Ensure the CSV has the necessary columns (`Content` for log messages and `EventId` for labels).

2. **Run the training script:**

   ```sh
   python fine_tune_bert.py
   ```

## Training Script

The training script `fine_tune_bert.py` performs the following steps:

1. Loads and inspects the dataset.
2. Defines a custom PyTorch dataset class.
3. Preprocesses the data, including tokenization and splitting into training and validation sets.
4. Creates data loaders for batching.
5. Sets the device to `mps` (if available) or `cpu`.
6. Loads a pre-trained BERT model with a classification head.
7. Defines training arguments and initializes the `Trainer` from Hugging Face's `transformers` library.
8. Trains and evaluates the model.
9. Saves the fine-tuned model and tokenizer.

## Example Dataset

Here is an example of the expected format for the dataset CSV file:

| LineId | Month | Date | Time | Level | Component | PID | Content                                                | EventId | EventTemplate                                        |
|--------|-------|------|------|-------|-----------|-----|--------------------------------------------------------|---------|------------------------------------------------------|
| 1      | Jun   | 14   | 15:16:01 | combo  | sshd(pam_unix) | 19939.0 | authentication failure; logname= uid=0 euid=0 ...       | E16     | authentication failure; logname= uid=0 euid=0 ...     |
| 2      | Jun   | 14   | 15:16:02 | combo  | sshd(pam_unix) | 19937.0 | check pass; user unknown                                | E27     | check pass; user unknown                              |

## Dependencies

- `pandas`
- `torch`
- `transformers`
- `scikit-learn`
- `torchaudio`
- `torchvision`

## Troubleshooting

- If you encounter issues with the MPS backend, ensure that you have macOS 12.3+ and PyTorch v1.12 or later installed.
- Use the environment variable `PYTORCH_ENABLE_MPS_FALLBACK=1` to enable CPU fallback for operations not yet implemented in MPS.

## License

This project is licensed under the MIT License. See the LICENSE file for more details.

## Acknowledgements

- Hugging Face for the `transformers` library.
- PyTorch for providing an excellent deep learning framework.
