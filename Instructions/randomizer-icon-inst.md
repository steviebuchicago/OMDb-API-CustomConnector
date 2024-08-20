# Creating a Randomizer in PowerApps

This repository provides detailed instructions on how to create a randomizer in PowerApps. A randomizer can be used to generate random values, such as selecting a random item from a list, generating random numbers, or any other scenario where randomness is required.

## Prerequisites

Before you start, ensure you have the following:

- A PowerApps account.
- A basic understanding of PowerApps controls and formulas.

## Step 1: Set Up the PowerApps Environment

### 1.1 Create or Open an App

1. Go to the [PowerApps portal](https://make.powerapps.com) and sign in with your account credentials.
2. You can either create a new Canvas app or open an existing app where you want to add the randomizer functionality.

### 1.2 Add a Data Source (Optional)

If your randomizer is going to select from a data source, make sure to add that data source to your app. For example, if you want to randomize items from a SharePoint list, Excel file, or other data sources, connect that data source to your app.

## Step 2: Create the Randomizer

### 2.1 Random Number Generation

1. **Add a Button:** Insert a button into your app where users can trigger the randomization process.

2. **Add a Label:** Insert a label that will display the random number.

3. **Set the OnSelect Property of the Button:**
   - In the button’s **OnSelect** property, add the following formula to generate a random number between 1 and 100:

   ```plaintext
   Set(varRandomNumber, RandBetween(1, 100))
   ```

   - Here, `varRandomNumber` is a variable that stores the generated random number. You can adjust the range (1 to 100) as needed.

4. **Display the Random Number:**
   - Set the **Text** property of the label to:

   ```plaintext
   varRandomNumber
   ```

   - This will display the random number generated when the button is clicked.

### 2.2 Random Item Selection from a List

1. **Create a Collection (Optional):**
   - If you want to randomize from a specific list of items (e.g., movie titles, names, etc.), you can create a collection in PowerApps:

   ```plaintext
   ClearCollect(myItems, ["Inception", "The Matrix", "Interstellar", "The Dark Knight", "Fight Club"])
   ```

   - This creates a collection named `myItems` containing movie titles.

2. **Add a Button:** Insert a button to trigger the random selection.

3. **Add a Label:** Insert a label that will display the randomly selected item.

4. **Set the OnSelect Property of the Button:**
   - In the button’s **OnSelect** property, add the following formula to select a random item from the collection:

   ```plaintext
   Set(varRandomItem, LookUp(myItems, Value = Last(FirstN(myItems, RandBetween(1, CountRows(myItems))))))
   ```

   - Here, `varRandomItem` stores the randomly selected item.

5. **Display the Random Item:**
   - Set the **Text** property of the label to:

   ```plaintext
   varRandomItem
   ```

   - This will display the randomly selected item when the button is clicked.

### 2.3 Randomize Across Multiple Data Sources (Advanced)

If you want to randomize across multiple data sources, such as combining two lists or databases, you can create a more complex randomizer by merging collections or using nested `RandBetween` and `LookUp` functions.

## Step 3: Test the Randomizer

### 3.1 Run Your App

1. Click the **Play** button to run your app in Preview mode.
2. Click the randomizer button to generate a random number or select a random item from the list.

### 3.2 Debugging

If the randomizer isn’t working as expected, check the following:

- Ensure all formulas are correct.
- Verify that any collections or data sources are properly initialized.
- Use the **Variables** pane in PowerApps to check if the random variables are being set correctly.

## Step 4: Deploy and Share Your App

### 4.1 Save and Publish

1. Once satisfied with the randomizer functionality, save your app.
2. Publish it to your organization if you want to share it with other users.

---

By following these instructions, you can create a functional randomizer in PowerApps, whether it's for generating random numbers, selecting random items from a list, or any other randomization needs within your app.

Feel free to customize this guide according to your specific use case or PowerApps environment.
