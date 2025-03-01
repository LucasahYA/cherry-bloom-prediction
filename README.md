# cherry-bloom-prediction

#### **Project Overview**
This project predicts cherry blossom bloom dates using meteorological data and machine learning models. The dataset is built from NOAA climate data, and features are engineered based on temperature accumulation, precipitation, and extreme weather conditions. The final model is trained using various regression techniques, with **ElasticNet** selected as the best-performing model.

---

### **Repository Structure**
- 📂 **`data_cleaning_preprocessing`**  
  - Preprocesses and cleans historical weather data.  
  - Removes long missing periods, fills gaps using rolling averages, and ensures continuous time series.  
  - Aligns data with a **seasonal year (March–next year's February)** for better feature extraction.  

- 📂 **`request_station_id`**  
  - Uses the NOAA API to find the nearest weather station ID based on bloom observation locations.  
  - Queries the **Global Historical Climatology Network (GHCND)** dataset.  

- 📂 **`request_weather`**  
  - Fetches historical daily weather records (TMAX, TMIN, PRCP) from NOAA using the retrieved station IDs.  
  - Aggregates data into a structured CSV format.  

- 📂 **`Training_Predicting`**  
  - Trains machine learning models (**Linear Regression, Ridge, Lasso, ElasticNet**) on processed weather data.  
  - Tunes hyperparameters using **GridSearchCV** and evaluates model performance.  
  - Predicts bloom **DOY (day of year)** for multiple locations.  

---

### **Data Processing Workflow**
1. **Fetch station IDs** for bloom observation locations using the NOAA API (`request_station_id`).
2. **Retrieve weather data** from NOAA for the identified stations (`request_weather`).
3. **Preprocess data** by filling missing values, removing non-continuous periods, and engineering features (`data_cleaning_preprocessing`).
4. **Train regression models** and optimize hyperparameters (`Training_Predicting`).
5. **Generate bloom predictions** for selected locations.

---

### **Feature Engineering**
- **Seasonal Temperature & Precipitation**: Aggregated Tmax, Tmin, and PRCP for Winter, Spring, Summer, and Fall.  
- **Growing Degree Days (GDD)**: Accumulated warmth above 5°C over 30, 60, and 120 days.  
- **Rolling Trends**: 7-day & 30-day temperature and precipitation trends.  
- **Extreme Weather Indicators**: Frost days (Tmin < 0°C), heat days (Tmax > 25°C).  

---

### **How to Run**
1. Clone the repository:
   ```bash
   git clone https://github.com/your-repo/cherry-blossom-prediction.git
   cd cherry-blossom-prediction
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. **Fetch station IDs**:
   ```bash
   python request_station_id.py
   ```
4. **Retrieve weather data**:
   ```bash
   python request_weather.py
   ```
5. **Preprocess data**:
   ```bash
   python data_cleaning_preprocessing.py
   ```
6. **Train models & make predictions**:
   ```bash
   python Training_Predicting.py
   ```

---

### **Model Selection**
- The final model chosen for prediction is **ElasticNet**, as it provided the best performance by balancing bias and variance.  
- Other models tested: **Linear Regression, Ridge Regression, Lasso Regression**.  

---

### **Prediction Results**
Example output:
```
(ElasticNet) The predicted bloom doy of Kyoto is: [92].
(ElasticNet) The predicted bloom doy of Washington DC is: [71].
(ElasticNet) The predicted bloom doy of New York City is: [89].
(ElasticNet) The predicted bloom doy of Liestal is: [110].
(ElasticNet) The predicted bloom doy of Vancouver is: [108].
```

---

### **Acknowledgment**
- **NOAA API** for historical weather data.
- **Cherry Blossom Watch** for bloom observation data.
- Machine learning models implemented using **scikit-learn**.

---

Let me know if you'd like to modify or add any details! 🚀
