# Expense Tracker (ReactJS)
## Date:24-05-2025

## AIM
To develop a simple Expense Tracker application using React that allows users to manage their personal finances by adding, viewing, and deleting income and expense transactions, while dynamically calculating the current balance, total income, and total expenses.

## ALGORITHM
### STEP 1: Initialize the Project
Create a new React app using:

npx create-react-app expense-tracker
or

npm create vite@latest expense-tracker --template react

Open the project in a code editor like VS Code.

### Step 2: Setup State
Define a state variable to store transactions:

Example: const [transactions, setTransactions] = useState([])

Define state variables for the form inputs:

const [text, setText] = useState("")

const [amount, setAmount] = useState("")

### Step 3: Add a New Transaction
Create a form with two inputs:

Text input for description

Number input for amount

On form submit:

Validate input

Create a new transaction object

Add the object to the transactions array using setTransactions.

### Step 4: Display Transaction List

Use map() to render each transaction in a list.

Conditionally style each item based on amount > 0 (income) or amount < 0 (expense).

Add a delete button next to each transaction.

### Step 5: Calculate and Display Summary

Use reduce() to calculate:

Total Balance: sum of all amounts

Total Income: sum of all positive amounts

Total Expenses: sum of all negative amounts

Display these values at the top of the UI.

### Step 6: Delete a Transaction

When delete is clicked:

Use filter() to remove the transaction from the array by id.

Update the state using setTransactions.

### Step 7: Style the Application

Use basic CSS to style:

Balance summary

Income/expense totals

Form inputs

Transaction list (with color coding)

## PROGRAM

app.jsx

```
app.js

import React, { useState } from 'react';
import './App.css';

function App() {
  const [transactions, setTransactions] = useState([]);
  const [text, setText] = useState('');
  const [amount, setAmount] = useState('');

  const addTransaction = (e) => {
    e.preventDefault();

    if (!text || !amount) return;

    const newTransaction = {
      id: Date.now(),
      text,
      amount: +amount,
    };

    setTransactions([newTransaction, ...transactions]);
    setText('');
    setAmount('');
  };

  const deleteTransaction = (id) => {
    setTransactions(transactions.filter((t) => t.id !== id));
  };

  const balance = transactions.reduce((acc, t) => acc + t.amount, 0).toFixed(2);
  const income = transactions
    .filter((t) => t.amount > 0)
    .reduce((acc, t) => acc + t.amount, 0)
    .toFixed(2);
  const expense = (
    transactions.filter((t) => t.amount < 0).reduce((acc, t) => acc + t.amount, 0) * -1
  ).toFixed(2);

  return (
    <div className="container">
      <h2> Expense Tracker</h2>
      <div className="balance">
        <h3>Your Balance</h3>
        <h1>₹{balance}</h1>
      </div>

      <div className="summary">
        <div>
          <h4>Income</h4>
          <p className="plus">+₹{income}</p>
        </div>
        <div>
          <h4>Expense</h4>
          <p className="minus">-₹{expense}</p>
        </div>
      </div>

      <form onSubmit={addTransaction}>
        <h3>Add New Transaction</h3>
        <input
          type="text"
          value={text}
          onChange={(e) => setText(e.target.value)}
          placeholder="Enter description..."
        />
        <input
          type="number"
          value={amount}
          onChange={(e) => setAmount(e.target.value)}
          placeholder="Enter amount (positive or negative)"
        />
        <button type="submit">Add Transaction</button>
      </form>

      <h3>History</h3>
      <ul className="list">
        {transactions.map((t) => (
          <li key={t.id} className={t.amount >= 0 ? 'plus' : 'minus'}>
            {t.text} <span>₹{t.amount}</span>
            <button onClick={() => deleteTransaction(t.id)}>❌</button>
          </li>
        ))}
      </ul>
    </div>
  );
}

export default App;
```
app.css

```
app.css

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: 'Segoe UI', sans-serif;
}

.container {
  max-width: 400px;
  margin: 30px auto;
  padding: 20px;
  background: #fff;
  border-radius: 10px;
  box-shadow: 0 0 10px #e2e2e2;
}

h2 {
  text-align: center;
  margin-bottom: 20px;
  color: #444;
}

.balance {
  text-align: center;
  margin: 20px 0;
}

.balance h1 {
  margin-top: 5px;
  color: #333;
}

.summary {
  display: flex;
  justify-content: space-between;
  margin: 20px 0;
  background: #f9f9f9;
  padding: 10px;
  border-radius: 5px;
}

.summary div {
  width: 48%;
  text-align: center;
}

.plus {
  color: green;
}

.minus {
  color: red;
}

form {
  display: flex;
  flex-direction: column;
}

form input {
  padding: 10px;
  margin: 10px 0;
  border: 1px solid #ddd;
  border-radius: 5px;
}

form button {
  padding: 10px;
  background: #ff69b4;
  color: white;
  font-weight: bold;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

form button:hover {
  background: #ff1493;
}

.list {
  list-style: none;
  margin-top: 10px;
}

.list li {
  background: #f5f5f5;
  margin: 10px 0;
  padding: 10px;
  border-right: 5px solid;
  border-radius: 5px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.list li.plus {
  border-color: green;
}

.list li.minus {
  border-color: red;
}

.list button {
  background: transparent;
  border: none;
  color: #aaa;
  font-size: 16px;
  cursor: pointer;
}

.list button:hover {
  color: red;
}
```
## OUTPUT

![WhatsApp Image 2025-05-24 at 11 17 56_c8c19a26](https://github.com/user-attachments/assets/3d3fee1c-f64d-43af-8fc3-1cd489449e15)

## RESULT
A fully functional React-based Expense Tracker application was successfully developed. 
