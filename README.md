const products = [
    {
      id: 101,
      title: "Sony LED 40 inch",
      variations: [
        { color: "black", price: 50000, quantity: 5 },
        { color: "gray", price: 45000, quantity: 4 },
        { color: "black", price: 48000, quantity: 5 }
      ],
      reviews: [
        { rating: 5.0, status: true },
        { rating: 4.0, status: true },
        { rating: 4.5, status: true }
      ]
    },
    {
      id: 102,
      title: "Mobile",
      variations: [
        { color: "black", price: 25000, quantity: 2 },
        { color: "white", price: 26000, quantity: 0 }
      ],
      reviews: [
        { rating: 4.0, status: true },
        { rating: 4.0, status: false }
      ]
    },
    {
      id: 103,
      title: "Bike",
      variations: [
        { color: "red", price: 150000, quantity: 3 },
        { color: "black", price: 160000, quantity: 1 }
      ],
      reviews: [
        { rating: 4.0, status: true },
        { rating: 4.0, status: true }
      ]
    }
  ];
//   ***************************************************
// Use map to get an array of product titles
const productTitles = products.map(product => product.title);
console.log(productTitles);
// Output: ["Sony LED 40 inch", "Mobile", "Bike"]


// ***********************************************************

// Use filter to get all products that have variations in black color
const blackProducts = products.filter(product => 
    product.variations.some(variation => variation.color === "black")
  );
  console.log(blackProducts);
  // Output will include all products since all have at least one black variation

// *********************************************************

// Use reduce to calculate the total stock of all products

const totalStock = products.reduce((sum, product) => 
    sum + product.variations.reduce((productSum, variation) => 
      productSum + variation.quantity, 0), 0);
  console.log(totalStock);
  // Output: 20

// **************************************************************

// Use map and reduce to get the average rating of each product


const averageRatings = products.map(product => {
    const validReviews = product.reviews.filter(review => review.status);
    const totalRating = validReviews.reduce((sum, review) => sum + review.rating, 0);
    const avg = validReviews.length ? totalRating / validReviews.length : 0;
    return {
      title: product.title,
      averageRating: avg
    };
  });
  console.log(averageRatings);
  // Output: [
  //   { title: "Sony LED 40 inch", averageRating: 4.5 },
  //   { title: "Mobile", averageRating: 4.0 },
  //   { title: "Bike", averageRating: 4.0 }
  // ]

//   ****************************************

// Use filter to get products that have at least one review with a rating of 5.0


// Find products that contain at least one review with a 5-star rating.


const fiveStarProducts = products.filter(product => 
    product.reviews.some(review => review.rating === 5.0)
  );
  console.log(fiveStarProducts);
  // Output: [ { id: 101, title: "Sony LED 40 inch", ... } ]

//   ***********************************************

// Use map to format variations with product name

const formattedProducts = products.map(product => ({
    title: product.title,
    variations: product.variations.map(variation => ({
      color: variation.color,
      price: variation.price,
      quantity: variation.quantity
    }))
  }));
  console.log(formattedProducts);
  // Output will show each product with title and its variations

//   ************************************************

// Use reduce to get the total revenue if all items were sold

const totalRevenue = products.reduce((sum, product) => 
    sum + product.variations.reduce((productSum, variation) => 
      productSum + (variation.price * variation.quantity), 0), 0);
  console.log(totalRevenue);
  // Output: 850000

//   **************************************************

// Use map to get a summary of each product with total variations and total reviews

const productSummaries = products.map(product => ({
    title: product.title,
    totalVariations: product.variations.length,
    totalReviews: product.reviews.length
  }));
  console.log(productSummaries);
  // Output: [
  //   { title: "Sony LED 40 inch", totalVariations: 3, totalReviews: 3 },
  //   { title: "Mobile", totalVariations: 2, totalReviews: 2 },
  //   { title: "Bike", totalVariations: 2, totalReviews: 2 }
  // ]

//   *******************************************************

// Use reduce to find the product with the highest total stock

const productWithHighestStock = products.reduce((maxProduct, currentProduct) => {
    const currentStock = currentProduct.variations.reduce((sum, variation) => 
      sum + variation.quantity, 0);
    const maxStock = maxProduct.variations.reduce((sum, variation) => 
      sum + variation.quantity, 0);
    return currentStock > maxStock ? currentProduct : maxProduct;
  });
  
  const result = {
    title: productWithHighestStock.title,
    totalStock: productWithHighestStock.variations.reduce((sum, variation) => 
      sum + variation.quantity, 0)
  };
  console.log(result);
  // Output: { title: "Sony LED 40 inch", totalStock: 14 }

//   **************************************************


//  the end 

