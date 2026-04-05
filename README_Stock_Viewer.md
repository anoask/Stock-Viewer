# Stock Viewer

A Windows Forms stock analysis application built in C# and .NET Framework 4.8 for viewing OHLCV market data from CSV files, filtering by date range, and identifying common candlestick patterns.

## Overview

This project loads stock price data from CSV files and displays it in an interactive candlestick chart. It also computes derived candlestick features and highlights recognized chart patterns such as Doji, Hammer, Engulfing, Harami, Peak, and Valley.

The app supports opening multiple files at once. The first selected file is shown in the main window, and each additional file opens in its own child window with the same date range so you can compare stocks side by side.

## Features

- Load one or more stock CSV files through a file picker
- Display OHLCV data in a candlestick chart
- Filter visible data using start and end date pickers
- Automatically normalize chart bounds based on the loaded data
- Detect and annotate candlestick patterns on the chart
- Open multiple stock files in separate windows for comparison
- Parse historical stock data from Yahoo Finance-style CSV format

## Recognized Patterns

The project includes recognizers for these patterns:

- Bullish
- Bearish
- Neutral
- Marubozu
- Hammer
- Doji
- Dragonfly Doji
- Gravestone Doji
- Bullish Engulfing
- Bearish Engulfing
- Bullish Harami
- Bearish Harami
- Peak
- Valley

Single-candle and multi-candle patterns are marked directly on the chart using arrows and dashed rectangles.

## Tech Stack

- C#
- Windows Forms
- .NET Framework 4.8
- `System.Windows.Forms.DataVisualization`

## Project Structure

```text
Stock-Viewer-main/
├── App.config
├── Candlestick.cs                  # Base OHLCV model parsed from CSV
├── SmartCandlestick.cs             # Derived candlestick metrics + pattern dictionary
├── Form_StockViewer.cs             # Main UI logic, file loading, filtering, charting
├── Form_StockViewer.Designer.cs    # Windows Forms layout
├── Recognizer.cs                   # Abstract base class for pattern recognizers
├── Recognizer_*.cs                 # Individual pattern detection implementations
├── Program.cs                      # Application entry point
└── WindowsFormsApp COP 4365.csproj # Project file
```

## How It Works

### 1. CSV parsing
Each row is read into a `Candlestick` object with these fields:

- Date
- Open
- High
- Low
- Close
- Volume

### 2. Feature engineering
Each `SmartCandlestick` computes extra properties used for recognition:

- Total range
- Top and bottom price
- Body range
- Upper tail
- Lower tail

### 3. Pattern recognition
A dictionary of recognizer classes evaluates every candlestick or candlestick group and stores boolean pattern matches.

### 4. Visualization
The filtered dataset is bound to a candlestick chart. When a pattern is chosen in the combo box, matching candles are annotated on the chart.

## Expected CSV Format

The reader expects the first line of the file to match this exact header:

```csv
Date,Open,High,Low,Close,Adj Close,Volume
```

Example row:

```csv
2024-01-02,185.64,188.44,183.89,187.32,187.32,82488700
```

## How to Run

### Option 1: Visual Studio
1. Open `WindowsFormsApp COP 4365.csproj` in Visual Studio.
2. Make sure the target framework is .NET Framework 4.8.
3. Build and run the project.
4. Click **Open File** and choose one or more supported CSV files.

### Option 2: Run the included executable
A debug executable is already present in:

```text
bin/Debug/WindowsFormsApp COP 4365.exe
```

You may need the matching .NET Framework installed on your machine.

## Usage

1. Launch the app.
2. Click **Open File**.
3. Select one or more stock CSV files.
4. Adjust the **start date** and **end date** if needed.
5. Click **Update** to refresh the view.
6. Choose a pattern from the dropdown to overlay annotations on the chart.

## Notes

- The file picker is configured for monthly, weekly, and daily CSV naming patterns.
- The default file dialog directory is hardcoded to a local Windows path and may need adjustment on another machine.
- The repository currently includes `bin/` and `obj/` build artifacts, which are usually excluded in source control.

## Possible Improvements

- Add import support for more CSV providers
- Add moving averages and technical indicators
- Add zooming, panning, and tooltip details
- Export detected pattern results to CSV
- Improve error handling for malformed files
- Add tests for recognizer logic
- Add screenshots directly to the repo instead of external image links

## Existing Screenshots

These were included in the original repository README:

- ![Screenshot 1](https://github.com/user-attachments/assets/65232737-da7d-4491-8c92-4b25d380aa47)
- ![Screenshot 2](https://github.com/user-attachments/assets/ebd7e1e8-3ee9-4407-9b38-2962752e9c90)
- ![Screenshot 3](https://github.com/user-attachments/assets/547ae041-ec82-4e65-af40-173bd16ba250)
- ![Screenshot 4](https://github.com/user-attachments/assets/360f20b4-9794-44f5-875b-67e188d5e963)

## License

No license file is currently included in the project.
