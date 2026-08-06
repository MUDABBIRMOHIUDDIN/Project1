//SDC 

//exp1

import React, { useState } from "react";

function App() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h1>JSX and Virtual DOM Demo</h1>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>
    </div>
  );
}

export default App;

//exp2

import React from "react";
import ProductCard from "./ProductCard";

const products = [
  { id: 1, name: "Laptop", price: 75000, category: "Electronics" },
  { id: 2, name: "Shoes", price: 2500, category: "Fashion" },
  { id: 3, name: "Watch", price: 5000, category: "Accessories" },
];

function App() {
  const handleBuyNow = (productName) => {
    alert(`You clicked Buy Now for ${productName}`);
  };

  return (
    <div style={{ textAlign: "center" }}>
      <h1>🛍️ Product Listing Page</h1>

      <div
        style={{
          display: "flex",
          justifyContent: "center",
          gap: "20px",
        }}
      >
        {products.map((product) => (
          <ProductCard
            key={product.id}
            name={product.name}
            price={product.price}
            category={product.category}
            onBuy={() => handleBuyNow(product.name)}
          />
        ))}
      </div>
    </div>
  );
}

export default App;

import React from "react";

function ProductCard({ name, price, category, onBuy }) {
  return (
    <div
      style={{
        border: "1px solid #ccc",
        padding: "15px",
        borderRadius: "8px",
        width: "200px",
      }}
    >
      <h3>{name}</h3>
      <p>Category: {category}</p>
      <p>Price: ₹{price}</p>
      <button onClick={onBuy}>Buy Now</button>
    </div>
  );
}

export default ProductCard;

//exp3

import React, { useState, useMemo } from "react";

export default function App() {
  const [products] = useState([
    { name: "Pen", qty: 10, price: 20 },
    { name: "Book", qty: 5, price: 100 },
  ]);

  const [search, setSearch] = useState("");
  const [dark, setDark] = useState(false);

  const totalValue = useMemo(() => {
    return products.reduce(
      (sum, item) => sum + item.qty * item.price,
      0
    );
  }, [products]);

  const filtered = products.filter((p) =>
    p.name.toLowerCase().includes(search.toLowerCase())
  );

  return (
    <div
      style={{
        backgroundColor: dark ? "black" : "white",
        color: dark ? "white" : "black",
        minHeight: "100vh",
        padding: "20px",
      }}
    >
      <h2>Inventory Management</h2>

      <button onClick={() => setDark(!dark)}>
        Toggle Theme
      </button>

      <br />
      <br />

      <input
        type="text"
        placeholder="Search Product"
        value={search}
        onChange={(e) => setSearch(e.target.value)}
      />

      <ul>
        {filtered.map((p, index) => (
          <li key={index}>
            {p.name} - Qty: {p.qty} - ₹{p.price}
          </li>
        ))}
      </ul>

      <h3>Total Value: ₹{totalValue}</h3>
    </div>
  );
}


//stm

//dependencies
<dependencies>

<dependency>
    <groupId>org.seleniumhq.selenium</groupId>
    <artifactId>selenium-java</artifactId>
    <version>4.25.0</version>
</dependency>
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <version>2.4.240</version>
</dependency>


//exp2
package com.test.selenium;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class Exp2_SinglePropertyCheckpoint {

    public static void main(String[] args) throws InterruptedException {

        

    	WebDriver driver=new ChromeDriver();
    	driver.get("https://google.com");
    	
    	String expectedTitle="Google";
    	
    	String actualTitle=driver.getTitle();
    	System.out.println("Actual Title : " + actualTitle);
      System.out.println("Expected Title : " + expectedTitle);


      if(actualTitle.equals(expectedTitle)) {
          System.out.println("PASS: Title is correct");
      }
      else {
          System.out.println("FAIL: Title is incorrect");
      }
      Thread.sleep(2000);
      driver.quit();
    	
    	
    }
}

//exp3
package com.test.selenium;

import java.time.Duration;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;

public class Exp3_SingleObjectCheckpoint {

    public static void main(String[] args) {


    	WebDriver driver = new ChromeDriver();
    	driver.get("https://google.com");
    	WebDriverWait wait = new WebDriverWait(driver,Duration.ofSeconds(10));
    	WebElement searchbox = driver.findElement(By.name("q"));

    	boolean displayed=searchbox.isDisplayed();
    	boolean enabled=searchbox.isEnabled();
    	System.out.println("Displayed : " + displayed);
    	System.out.println("Enabled   : " + enabled);

    	if (displayed && enabled) {
    		System.out.println("PASS: Search box is ready");
    	} else {
          System.out.println("FAIL: Search box is not ready");
    	}

      // Close browser
      driver.quit();
    	
    }
}

//exp 4a

package com.test.selenium;

import org.openqa.selenium.*;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.io.FileHandler;

import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

public class Exp4_BitmapCheckpoint {

    public static void main(String[] args) {

        WebDriver driver = new ChromeDriver();

        try {

            driver.get("https://www.google.com");

            // Locate Google search box
            WebElement searchBox = driver.findElement(By.name("q"));

            // Create Screenshots folder
            File folder = new File("Screenshots");

            if (!folder.exists()) {
                folder.mkdir();
            }

            // Capture screenshot
            File source = searchBox.getScreenshotAs(OutputType.FILE);

            File currentFile =
                    new File("Screenshots/current_searchbox.png");

            FileHandler.copy(source, currentFile);

            System.out.println("Current Screenshot Saved");
            System.out.println(currentFile.getAbsolutePath());

            // Baseline Image
            File baselineFile =
                    new File("Screenshots/baseline_searchbox.png");

            if (!baselineFile.exists()) {

                System.out.println("Baseline image not found.");

                System.out.println(
                        "Rename current_searchbox.png to baseline_searchbox.png");

            } else {

                boolean result =
                        compareImages(baselineFile, currentFile);

                if (result) {

                    System.out.println(
                            "BITMAP CHECKPOINT : TEST PASS");

                    System.out.println(
                            "Images are identical.");

                } else {

                    System.out.println(
                            "BITMAP CHECKPOINT : TEST FAIL");

                    System.out.println(
                            "Images are different.");
                }

            }

        } catch (Exception e) {

            e.printStackTrace();

        } finally {

            driver.quit();

        }

    }

    // Compare images pixel by pixel

    public static boolean compareImages(File img1,
                                        File img2) throws Exception {

        BufferedImage image1 = ImageIO.read(img1);

        BufferedImage image2 = ImageIO.read(img2);

        if (image1.getWidth() != image2.getWidth()
                || image1.getHeight() != image2.getHeight()) {

            return false;

        }

        for (int x = 0; x < image1.getWidth(); x++) {

            for (int y = 0; y < image1.getHeight(); y++) {

                if (image1.getRGB(x, y)
                        != image2.getRGB(x, y)) {

                    return false;

                }

            }

        }

        return true;

    }

}

//exp 4b

package com.test.selenium;

import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

import org.openqa.selenium.OutputType;
import org.openqa.selenium.TakesScreenshot;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class Exp4b_BitmapCheckpoint {

    public static void main(String[] args) throws Exception {

        WebDriver driver = new ChromeDriver();

        try {
            // Maximize browser
            driver.manage().window().maximize();

            // Open Google
            driver.get("https://www.google.com");

            // Wait for page to load
            Thread.sleep(3000);

            // Capture full browser screenshot
            File screenshot = ((TakesScreenshot) driver).getScreenshotAs(OutputType.FILE);
            BufferedImage fullImage = ImageIO.read(screenshot);

            // Create folder if it doesn't exist
            File folder = new File("C:\\SeleniumScreenshots");
            if (!folder.exists()) {
                folder.mkdirs();
            }

            // Crop top-left area (800 x 600)
            int width = Math.min(800, fullImage.getWidth());
            int height = Math.min(600, fullImage.getHeight());

            BufferedImage currentArea = fullImage.getSubimage(0, 0, width, height);

            // Save cropped image
            File currentFile = new File("C:\\SeleniumScreenshots\\current_google_area.png");
            ImageIO.write(currentArea, "png", currentFile);

            System.out.println("Current screenshot saved:");
            System.out.println(currentFile.getAbsolutePath());

            // Baseline image
            File baselineFile = new File("C:\\SeleniumScreenshots\\baseline_google_area.png");

            if (!baselineFile.exists()) {

                System.out.println("Baseline image not found.");
                System.out.println("Rename current_google_area.png to baseline_google_area.png");

            } else {

                BufferedImage baseline = ImageIO.read(baselineFile);

                double similarity = compareImages(baseline, currentArea);

                System.out.println("Image Similarity : " + similarity + "%");

                if (similarity >= 95) {
                    System.out.println("BITMAP CHECKPOINT : TEST PASS");
                } else {
                    System.out.println("BITMAP CHECKPOINT : TEST FAIL");
                }
            }

        } finally {
            driver.quit();
        }
    }

    // Compare two images
    public static double compareImages(BufferedImage img1, BufferedImage img2) {

        if (img1.getWidth() != img2.getWidth() ||
            img1.getHeight() != img2.getHeight()) {
            return 0;
        }

        long totalPixels = (long) img1.getWidth() * img1.getHeight();
        long samePixels = 0;

        for (int x = 0; x < img1.getWidth(); x++) {
            for (int y = 0; y < img1.getHeight(); y++) {

                if (img1.getRGB(x, y) == img2.getRGB(x, y)) {
                    samePixels++;
                }

            }
        }

        return ((double) samePixels / totalPixels) * 100;
    }
}

//exp 5

package com.test.selenium;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class Exp5_DatabaseCheckpoint {

    public static void main(String[] args) {

        try {

            // Connect to H2 Database
            Connection con = DriverManager.getConnection(
                    "jdbc:h2:./StudentDB", "sa", "");

            Statement stmt = con.createStatement();

            // Create table
            stmt.execute(
                    "CREATE TABLE IF NOT EXISTS STUDENT (" +
                    "ID INT PRIMARY KEY, " +
                    "NAME VARCHAR(50), " +
                    "EMAIL VARCHAR(100))");

            // Delete previous data
            stmt.execute("DELETE FROM STUDENT");

            // Insert record
            stmt.executeUpdate(
                    "INSERT INTO STUDENT VALUES " +
                    "(1,'Ajay','ajay@gmail.com')");

            // Database Checkpoint
            ResultSet rs =
                    stmt.executeQuery(
                    "SELECT * FROM STUDENT WHERE ID = 1");

            if (rs.next()) {

                System.out.println("Record Exists");
                System.out.println("ID : " + rs.getInt("ID"));
                System.out.println("Name : " + rs.getString("NAME"));
                System.out.println("Email : " + rs.getString("EMAIL"));

                System.out.println("TEST PASSED");

            } else {

                System.out.println("Record Not Found");
                System.out.println("TEST FAILED");

            }

            rs.close();
            stmt.close();
            con.close();

        } catch (Exception e) {

            e.printStackTrace();

        }

    }

}



