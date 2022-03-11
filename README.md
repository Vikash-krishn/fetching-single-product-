



 I added all the product details in hashmap. I want to display the product details based on category. It means all same category products should be display. I am trying to create method for that. The method name is

public List<Product> getProductsBasedOnCategory(String category)
{

}
Please find below code.

Product.java

public class Product {

    private long pid;
    private String pname;
    private String category;
    private float price;
    private long stock;
    private String remarks;

    public Product()
    {

    }

    public Product(long pid,String pname,String category,float price,long stock,String remarks){
        this.pid=pid;
        this.pname=pname;
        this.category=category;
        this.price=price;
        this.stock=stock;
        this.remarks=remarks;
    }
    public long getPid() {
        return pid;
    }
    public void setPid(long pid) {
        this.pid = pid;
    }
    public String getPname() {
        return pname;
    }
    public void setPname(String pname) {
        this.pname = pname;
    }
    public String getCategory() {
        return category;
    }
    public void setCategory(String category) {
        this.category = category;
    }
    public float getPrice() {
        return price;
    }
    public void setPrice(float price) {
        this.price = price;
    }
    public long getStock() {
        return stock;
    }
    public void setStock(long stock) {
        this.stock = stock;
    }
    public String getRemarks() {
        return remarks;
    }
    public void setRemarks(String remarks) {
        this.remarks = remarks;
    }

}
DatabaseClass.java

public class DatabaseClass {

    private static Map<Long, Product> products=new HashMap<>();

    public static Map<Long, Product> getProduct()
    {
        return products;
    }

}
ProductDao.java

private Map<Long, Product> products=DatabaseClass.getProduct();

public ProductDaoImpl()
{
    products.put(1L, new Product(1L,"TV","Entertinement",10000F,250L,"This is best TV!"));
    products.put(2L, new Product(2L,"Computer","Technology",20000F,350L,"My Computer name Hp and SONY ViVo!"));
    products.put(3L, new Product(3L,"DeskTopComputer","Technology",15000F,150L,"My Desktop Computer name Accer and SONY ViVo!"));
}

//Get All products
public List<Product> getAllProducts() {

    return new ArrayList<Product>(products.values());
}

//Get product by product id
public Product getProduct(long pid) {

    return products.get(pid);
}

//To Add the products 
public Product addProduct(Product product) {
    product.setPid(products.size()+1);
    products.put(product.getPid(), product);
    return product;
}

//Update the product
public Product updateProduct(Product product) {
    if(product.getPid()<=0)
    {
        return null;
    }
    products.put(product.getPid(), product);
    return product;
}

// Delete the product
public Product deleteProduct(long pid) {

    return products.remove(pid);

}



//Get the product by category
public List<Product> getProductByCategory(String category) {

    if(products.size()<=0)
    {
        return null;
    }

    else if(category.equals(products.get(Product))
    {



    }
I am trying a lot how to write code to get the value of model class in HashMap.  getProductByCategory(String category).


 iterate over the set of values in the map, and filter to return the list of matching products:

public List<Product> getProductByCategory(String category) {

    if(products.size() == 0){
        return new ArrayList<>();
    }

    return this.products.values().stream()
       .filter(product -> product.getCategory().equals(category))
       .collect(Collectors.toList());
}
You can also use a for-loop for that:

public List<Product> getProductByCategory(String category) {

    List<Product> ret = new ArrayList<>();

    if(products.size() == 0){
        return ret;
    }

    for(Product p: this.products.values()) {
        if(p.getCategory().equals(category))
            ret.add(p);
    }

    return ret;
}

I return an empty ArrayList if the product map is empty. This is better practice for collection return types (instead of returning null)

One way is to iterate over the Hashmap --

public List<Product> getProductsBasedOnCategory(String category)
{
    List<Product> list = new ArrayList<Product>();

    if (products.size()<=0) {
        return list;
    }

    products.entrySet().stream().forEach((entry) -> {
        if (((Product) entry.getValue()).getCategory().equals(category)) {
            list.add(entry.getValue())
        }
    });

    return list;

}



Declare the maps

private Map<Long, Product> productsByID = new HashMap();
private Map<String, Product> productsByCategory = new HashMap();
Initialize the maps

public ProductDaoImpl()
{
    // Create the objects
    Product p1 = new Product(1L,"TV","Entertinement",10000F,250L,"This is best TV!");
    Product p2 = new Product(2L,"Computer","Technology",20000F,350L,"My Computer name Hp and SONY ViVo!");
    Product p3 = new Product(3L,"DeskTopComputer","Technology",15000F,150L,"My Desktop Computer name Accer and SONY ViVo!");

    //Assign the objects into the map by ids
    productsByID.put(1L, p1);
    productsByID.put(2L, p2);
    productsByID.put(3L, p3);

    //Assign the objects into the map by category
    productsByCategory.put(p1.getCategory(), p1);
    productsByCategory.put(p2.getCategory(), p2);
    productsByCategory.put(p3.getCategory(), p3);
}


 
