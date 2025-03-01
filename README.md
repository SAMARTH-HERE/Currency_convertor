# Currency Converter App

This is a simple currency converter application built using React. The app allows users to convert an amount from one currency to another based on the latest exchange rates.

## Features

- Convert amounts between different currencies
- Swap currencies easily with a single click
- Dynamic fetching of currency exchange rates
- Responsive and user-friendly interface

## Getting Started

### Prerequisites

- Node.js (v14 or later)
- npm (v6 or later) or yarn (v1.22 or later)

### Installation

1. Clone the repository:

```bash
git clone https://github.com/yourusername/currency-converter.git
cd currency-converter
```

2. Install the dependencies:

```bash
npm install
# or
yarn install
```

### Running the App

To start the development server:

```bash
npm run dev
# or
yarn dev
```

Open your browser and go to `http://localhost:3000` to see the app in action.

## Usage

1. Enter the amount you want to convert.
2. Select the currency you are converting from.
3. Select the currency you are converting to.
4. Click on the "Convert" button to see the converted amount.
5. Use the "Swap" button to switch the currencies and convert again.

## Components

### App.jsx

The main component that handles the state and logic of the currency converter.

```javascript
import { useState } from 'react';
import reactLogo from './assets/react.svg';
import viteLogo from '/vite.svg';
import './App.css';
import InputBox from './components/InputBox';
import useCurrencyInfo from "./hooks/useCurrencyInfo";

function App() {
  const [amount, setAmount] = useState(0);
  const [from, setFrom] = useState("usd");
  const [to, setTo] = useState("inr");
  const [convertedAmount, setConvertedAmount] = useState(0);

  const currencyInfo = useCurrencyInfo(from);
  const options = Object.keys(currencyInfo);

  const swap = () => {
    setFrom(to);
    setTo(from);
    setAmount(convertedAmount);
    setConvertedAmount(amount);
  };

  const converted = () => {
    setConvertedAmount(amount * currencyInfo[to]);
  };

  return (
    <div className='w-full h-screen flex flex-wrap justify-center item-center bg-cover bg-no-repeat' style={{backgroundImage:'url("https://images.unsplash.com/photo-1720599020164-002f9626d55c?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D")'}}>
      <div className='w-full'>
        <br /><br />
        <h1>Currency Converter</h1>
        <br />
        <div className='w-full max-w-md mx-auto border-4 border-black rounded-lg p-10 backdrop-blur-sm bg-white '>
          <form onSubmit={(e) => { e.preventDefault(); converted(); }}>
            <br /><br /><br />
            <div className='w-full mb-1'>
              <InputBox
                label="From"
                amount={amount}
                currencyOptions={options}
                onCurrencyChange={(currency) => setAmount(amount)}
                selectCurrency={from}
                onAmountChange={(amount) => setAmount(amount)}
              />
              <br />
            </div>
            <div className='w-full relative h-0.5'>
              <button
                type="button"
                className="h-10 rounded-lg bg-yellow-200"
                onClick={swap}
              >
                Click here to swap
              </button>
            </div>
            <div className='w-full mt-1 mb-4'>
              <br /><br />
              <InputBox
                label="To"
                amount={convertedAmount}
                currencyOptions={options}
                selectCurrency={to}
              />
            </div>
            <button type="submit" className="w-full bg-blue-600 text-white px-4 py-3 rounded-lg">
              Convert {from.toUpperCase()} to {to.toUpperCase()}
            </button>
            <br /><br /><br />
          </form>
        </div>
      </div>
    </div>
  );
}

export default App;
```

### InputBox.jsx

A reusable input component for selecting currencies and entering amounts.

```javascript
import React, { useId } from 'react';

function InputBox({
  label,
  amount,
  onAmountChange,
  onCurrencyChange,
  currencyOptions = [],
  selectCurrency = "usd",
  amountDisable = false,
  currencyDisable = false,
  className = "",
}) {
  const amountInputId = useId();

  return (
    <div className={`bg-yellow-300 p-3 rounded-lg text-sm flex ${className}`}>
      <div className="w-1/2">
        <label htmlFor={amountInputId} className="text-black/40 mb-2 inline-block">
          {label}
        </label>
        <input
          id={amountInputId}
          className="outline-none w-full bg-transparent py-1.5"
          type="number"
          placeholder="Amount"
          disabled={amountDisable}
          value={amount}
          onChange={(e) => onAmountChange && onAmountChange(Number(e.target.value))}
        />
      </div>
      <div className="w-1/2 flex flex-wrap justify-end text-right">
        <p className="text-black/40 mb-2 w-full">Currency Type</p>
        <select
          className="rounded-lg px-1 py-1 bg-gray-100 cursor-pointer outline-none"
          value={selectCurrency}
          onChange={(e) => onCurrencyChange && onCurrencyChange(e.target.value)}
          disabled={currencyDisable}
        >
          {currencyOptions.map((currency) => (
            <option key={currency} value={currency}>
              {currency}
            </option>
          ))}
        </select>
      </div>
    </div>
  );
}

export default InputBox;
```

## Contributing

If you want to contribute to this project, feel free to open a pull request or an issue on the GitHub repository.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

