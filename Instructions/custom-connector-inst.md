# PowerApps Custom Connector for OMDb API

This repository provides detailed instructions on how to create a custom connector in PowerApps to connect to the OMDb API, and how to use it within your app as a "Run" action.

## **Prerequisites**

Before you start, ensure you have the following:

- A valid [OMDb API key](http://www.omdbapi.com/apikey.aspx).
- A PowerApps account with access to create custom connectors.

## **Step 1: Create a New Custom Connector in PowerApps**

### 1.1 **Sign in to PowerApps**
1. Go to the [PowerApps portal](https://make.powerapps.com) and sign in with your account credentials.
2. In the left navigation pane, expand the **Dataverse** section and select **Custom Connectors**.

### 1.2 **Create a New Connector**
1. Click **+ New custom connector** and choose **Create from blank**.
2. Provide a **Name** for your connector, such as `OMDb API Connector`.

### 1.3 **Set Up the General Information**
1. **Icon & Description:** Optionally, upload an icon for the connector and provide a brief description.
2. **Host:** Enter `www.omdbapi.com`.
3. **Base URL:** Enter `/`.

## **Step 2: Configure Security Settings**

### 2.1 **Choose Authentication Type**
1. Go to the **Security** tab.
2. Select **API Key** as the authentication type.
3. Under **Parameter Label**, enter `apikey`.
4. Set the **Parameter Name** to `apikey`.
5. For **Location**, choose **Query** (since OMDb API key is passed as a query parameter).

## **Step 3: Define Actions**

### 3.1 **Create a Search Movies Action**
1. Go to the **Definition** tab and click **+ New Action**.
2. Set the **Summary** to `Search for Movies`.
3. Set the **Operation ID** to `searchMovies`.
4. Provide a brief **Description**.

### 3.2 **Configure Request for Search Movies**
1. Under **Request**, click **Import from sample**.
2. Set the **Verb** to `GET`.
3. Enter the following **URL**:
   ```
   /?s={movieName}&apikey={your_api_key}
   ```
4. Under **Query Parameters**, click **+ Add default**:
   - **Parameter name:** `s`
   - **Parameter location:** Query
   - **Parameter type:** String
   - **Is required:** Yes (checked)

### 3.3 **Configure Response for Search Movies**
1. Under **Response**, click **Add default response**.
2. Click **Import from sample** and use the sample JSON response you get from the OMDb API, such as:
   ```json
   {
     "Search": [
       {
         "Title": "Inception",
         "Year": "2010",
         "imdbID": "tt1375666",
         "Type": "movie",
         "Poster": "https://example.com/inception.jpg"
       }
     ],
     "totalResults": "1",
     "Response": "True"
   }
   ```
3. Click **Import** to set the response schema.

## **Step 4: Test the Custom Connector**

### 4.1 **Test the Connector**
1. Save the custom connector by clicking **Save**.
2. Go to the **Test** tab.
3. Use the **Test operation** section to verify the connector by providing a sample movie name and clicking **Test operation**.

## **Step 5: Use the Custom Connector in PowerApps as a Run Action**

### 5.1 **Add the Custom Connector as a Data Source**
1. In PowerApps, open or create an app where you want to use the OMDb API.
2. Go to the **Data** tab and click **+ Add data**.
3. Search for the custom connector you created (`OMDb API Connector`) and add it.

### 5.2 **Use the Connector in a Formula**
1. To trigger the connector as a "Run" action, you can call it in a formula. For example, use a button's `OnSelect` property to run a search:
   ```plaintext
   Set(varMovieData, OMDbAPIConnector.searchMovies({movieName: "Inception"}))
   ```
2. In this example, `OMDbAPIConnector.searchMovies` is the "Run" action that is triggered when the button is clicked. The result is stored in a variable `varMovieData`.

### 5.3 **Display the Results**
1. You can now use the `varMovieData` variable to bind data to controls such as galleries or text labels.
   ```plaintext
   Gallery1.Items = varMovieData.Search
   ```
2. This will display the search results from the OMDb API in the gallery.

## **Step 6: Deploy and Share the Connector**

### 6.1 **Deploy the Connector**
1. Once you are satisfied with the custom connector, deploy it to your environment.
2. Share it with other users or apps in your organization as needed.

---

By following these instructions, you will have a custom connector integrated into your PowerApps application, allowing you to trigger API calls using the "Run" action and display movie data dynamically within your app.

Feel free to customize this guide according to your specific use case or PowerApps environment.
