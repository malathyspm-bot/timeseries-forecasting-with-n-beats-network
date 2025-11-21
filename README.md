# timeseries-forecasting-with-n-beats-network
1. DependenciesThe following packages are required to run the notebook:Bash# Core numerical and data analysis libraries
pip install torch torchvision torchaudio
pip install matplotlib pandas numpy scikit-learn statsmodels
# Optimization and utilities
pip install optuna tqdm joblib
The exact versions used were specified as: torch (2.8.0), statsmodels (0.14.5), and optuna (4.6.0).2. File StructureThe project will generate a simple output structure:.
├── Untitled7.ipynb          # The main comparison notebook
└── output/
    ├── arima_model.joblib   # Saved SARIMA model object
    └── nbeats_model.pt      # Saved N-BEATS model weights
The SARIMA model is saved using joblib.dump.📈 Performance ComparisonThe models were evaluated on the test set, forecasting 24 steps (one full day) ahead, based on an input window of 64 steps.The results show that the N-BEATS model significantly outperformed the optimized SARIMA model on the synthetic data.MetricN-BEATSARIMAMAE0.605117.2026RMSE0.753717.3423sMAPE0.7158NaNKey Findings:SARIMA struggled with the complexity of the synthetic series, resulting in a high Mean Absolute Error (MAE) of 17.2026.N-BEATS demonstrated superior performance, achieving a very low MAE of 0.6051.The optimal SARIMA parameters found via Optuna were not sufficient to capture the series' underlying structure.🔬 Model DetailsSARIMADifferencing Orders:Non-Seasonal Differencing (d): 1.Seasonal Differencing (D): 0 (with a seasonal period m=24).Hyperparameter Search: Performed using Optuna to minimize a performance metric on the validation set.N-BEATSArchitecture: A stack of three blocks: one Trend block, one Seasonality block, and one Generic block.Basis Functions: Utilizes polynomials for the Trend block and Fourier series for the Seasonality block.Training: Trained using the Mean Squared Error (MSE) loss function.
