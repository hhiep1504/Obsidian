 - The benchmark will run on an edge device (Jetson Nano)
- It will use the CUHK03 dataset for testing
- You'll be testing pre-trained models, not training them
- You want to compare your model against other models

To implement this benchmark -> write code that:
- [x] Loads and preprocesses the CUHK03 dataset
- [x] Implements or imports the evaluation metrics
- [x] Runs your method and other comparison methods on the dataset
- [ ] Calculates and stores the performance metrics for each method
- [ ] Generates comparative visualizations (e.g., CMC curves, bar charts for mAP)


### Project structure
``` python
reid/ 
│ 
├── dataset/ 
│   └── cuhk03/ # Place CUHK03 dataset here 
│ 
├── models/ 
│   ├── __init__.py 
│   ├── bkai_model.py # Your YOLOv10-based model 
│   ├── osnet.py
│   ├── ...
│   └──# Other models for comparison 
│   
├── engine/
│   ├── __init__.py 
│   ├── engine.py 
│   ├── image/
│       ├──__init__.py 
│       ├── softmax.py
│       └── triplet.py
│  
├── utils/ 
│   ├── __init__.py 
│   ├── avgmeter.py 
│   ├── loggers.py 
│   ├── feature_extractor.py 
│   ├── model_complexity.py 
│   ├── tools.py 
│   ├── torchtools.py 
│   ├── reidtools.py 
│   └── rerank.py 
│ 
├── configs/ 
│   └── config.yaml # Configuration file 
│   
├── benchmark.py # Main benchmarking script 
├── requirements.txt 
└── README.md
```

- `benchmark.py`: This is the main script that runs the benchmarking process. It loads the models, processes the dataset, and computes the metrics.
- `configs/config.yaml`: This file contains the configuration for the benchmark, including paths to the dataset and model weights, and other settings.
- `utils/data_loader.py`: This file contains the `CUHK03Dataset` class, which handles loading and preprocessing the CUHK03 dataset.
- `utils/metrics.py`: This file contains functions to compute the evaluation metrics (mAP and CMC).
- `models/`: This directory should contain your model implementations. You'll need to implement `YourModel` (your YOLOv10-based model) and any other models you want to compare against.
- `requirements.txt`: This file lists the Python dependencies for the project.
