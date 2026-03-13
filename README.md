Footing Reinforcement Weight Calculator
Automated Rebar Weight from Plan & Schedule PDFs

README – Run Instructions, Assumptions, Limitations
This notebook is designed to calculate the total rebar weight from provided 'Plan PDF' and 'Footing Schedule PDF' documents. It automates the extraction of footing marks and counts from the plan, and rebar details (quantity, bar size, length) from the schedule, processes this data, and provides a total rebar weight.

Instructions
Run all cells sequentially: Start from the top and execute each code cell in order.
Upload PDFs: When prompted, upload your 'Plan PDF' and 'Footing Schedule PDF' files using the provided interactive widgets.
Review Outputs: Observe the printed dataframes and final rebar weight. The notebook will generate footing_counts.csv and rebar_weight_results.csv files, which can be downloaded.
Gemini API Key: Ensure your Gemini API Key is configured in Colab Secrets as GEMINI_API_KEY for primary PDF extraction functionality. If not configured, the notebook will fall back to pdfplumber where possible, but Gemini API is the recommended and primary method.
Assumptions
PDF Structure: It is assumed that the 'Plan PDF' contains footing marks in a recognizable format (e.g., 'F1', 'F01', 'F104') that can be extracted using regular expressions or interpreted by the Gemini API.
Schedule PDF Structure: The 'Footing Schedule PDF' is assumed to contain tabular data with columns for 'Mark', 'Footing Length', 'Footing Width', 'Footing Thickness', 'Rebar Bottom', and 'Rebar Top'. The rebar information within the 'Rebar Bottom' and 'Rebar Top' columns is expected to follow a pattern like (Qty) #BarSize (e.g., (6) #5).
Rebar Orientation: Rebar specified in the schedule (e.g., 'Rebar Bottom', 'Rebar Top') is assumed to run "EACH WAY, UNO" (each way, unless noted otherwise), meaning bars are present along both the length and width of the footing, with the same quantity and bar size. This results in two entries for each rebar specification per footing (one for length-direction bars, one for width-direction bars).
Units: Footing dimensions (length, width, thickness) and rebar lengths in the schedule are assumed to be in feet-inch format (e.g., 5'-0", 5'-6", 60"). These are converted to decimal feet for calculations.
Unit Weights: The notebook uses a comprehensive set of standard unit weights for rebar sizes #3 through #18 (lbs/ft) as defined internally.
Missing Entries: If a footing mark from the 'Plan PDF' does not have a corresponding rebar entry in the 'Footing Schedule PDF', its rebar weight contribution is explicitly assumed to be zero, and a warning is issued.
Default Multiplier: A default multiplier of 4 is used (representing top & bottom, each way) for rebar quantity calculation, unless explicitly parsed otherwise.
Limitations
PDF Parsing Robustness: While the Gemini API is used for enhanced interpretation, and pdfplumber provides a fallback, PDF table extraction and text parsing can still be sensitive to highly unusual or complex PDF layouts and formatting. Significant deviations from expected structures might require manual intervention or further refinement of extraction logic.
Gemini API Dependency: The primary extraction relies on the Gemini API. Issues with API access, rate limits, or unexpected model responses can affect performance and accuracy, triggering the pdfplumber fallback.
Complex Rebar Designs: The notebook currently assumes rebar runs "EACH WAY, UNO" and does not account for more complex rebar configurations like stirrups, hooks, or varying bar quantities/sizes along different dimensions that might be specified in more detailed schedules beyond a simple Qty #BarSize format.
Footing Thickness/Depth: The current rebar weight calculation does not explicitly use footing thickness or depth. This assumes rebar is appropriately placed within the footing as per design, but the model does not verify this structural aspect.
Image-based PDFs: If the PDFs are image-based (scanned documents without searchable text), pdfplumber will fail to extract text, and Gemini's ability to interpret will be limited to its OCR capabilities.
