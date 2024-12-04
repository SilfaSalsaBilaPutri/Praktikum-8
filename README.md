| Nama : | Silfa Salsa Bila Putri |
| --- | ---|
| NIM : | 312310607 |
| Kelas : | TI.23.A6 |

# Buatkan kode java dari Diagram Class berikut

![image](https://github.com/user-attachments/assets/b2dc700e-e9e8-4453-a9ea-91ff91655380)

- Class Customer
  ```
  import java.util.ArrayList;
  import java.util.List;

  public class Customerr {
    private String name;
    private String address;
    private List<Order> orders; // Relasi ke banyak Order

    public Customerr() {
        orders = new ArrayList<>();
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getAddress() {
        return address;
    }

    public void setAddress(String address) {
        this.address = address;
    }

    public List<Order> getOrders() {
        return orders;
    }

    public void addOrder(Order order) {
        orders.add(order);
    }
    }
    ```
  - Kelas ini merepresentasikan pelanggan yang memiliki atribut:
    
    name: Nama pelanggan, dan address: Alamat pelanggan.
    
  - Relasi
    
    berhubungan dengan Order dalam relasi one-to-many (1 pelanggan bisa memiliki banyak pesanan).
    
  - Metod
    
    addOrder(Order order) : Menambahkan pesanan ke daftar pesanan pelanggan.
    
- Class Order
  ```
  import java.util.ArrayList;
  import java.util.List;

  public class Order {
    private String date;
    private String status;
    private List<OrderDetail> orderDetails; // Relasi ke banyak OrderDetail
    private List<Payment> payments;        // Relasi ke banyak Payment

    public Order() {
        orderDetails = new ArrayList<>();
        payments = new ArrayList<>();
    }

    public String getDate() {
        return date;
    }

    public void setDate(String date) {
        this.date = date;
    }

    public String getStatus() {
        return status;
    }

    public void setStatus(String status) {
        this.status = status;
    }

    public List<OrderDetail> getOrderDetails() {
        return orderDetails;
    }

    public void addOrderDetail(OrderDetail detail) {
        orderDetails.add(detail);
    }

    public List<Payment> getPayments() {
        return payments;
    }

    public void addPayment(Payment payment) {
        payments.add(payment);
    }

    public double calcTotal() {
        double total = 0;
        for (OrderDetail detail : orderDetails) {
            total += detail.calcSubTotal();
        }
        return total;
    }

    public double calcWeight() {
        double totalWeight = 0;
        for (OrderDetail detail : orderDetails) {
            totalWeight += detail.calcWeight();
        }
        return totalWeight;
    }
    }
    ```
    - Kelas ini merepresentasikan sebuah pesanan yang memiliki atribut:
      
      date: Tanggal pembuatan pesanan.

      status: Status pesanan (misalnya Processing, Completed).
  
    - Relasi

      Berhubungan dengan OrderDetail dalam relasi one-to-many (1 pesanan memiliki banyak rincian pesanan).

      Berhubungan dengan Payment dalam relasi one-to-many (1 pesanan dapat memiliki lebih dari 1 pembayaran).
  
    - Metode

      calcSubTotal(): Menghitung total harga sebelum pajak.

      calcTax(): Menghitung total pajak.

      calcTotal(): Menghitung total harga setelah pajak.

      calcTotalWeight(): Menghitung total berat barang dalam pesanan.
  
- Class OrderDetail
    ```
    public class OrderDetail {
    private int quantity;
    private String taxStatus;
    private Item item; // Relasi ke Item

    public int getQuantity() {
        return quantity;
    }

    public void setQuantity(int quantity) {
        this.quantity = quantity;
    }

    public String getTaxStatus() {
        return taxStatus;
    }

    public void setTaxStatus(String taxStatus) {
        this.taxStatus = taxStatus;
    }

    public Item getItem() {
        return item;
    }

    public void setItem(Item item) {
        this.item = item;
    }

    public double calcSubTotal() {
        return item.getPriceForQuantity(quantity);
    }

    public double calcWeight() {
        return item.getShippingWeight() * quantity;
    }

    public double calcTax() {
        return item.getTax() * quantity;
    }
    }
    ```
    - Kelas ini merepresentasikan rincian setiap item dalam sebuah pesanan, dengan atribut:
      
      quantity: Jumlah item dalam pesanan.
      
      taxStatus: Status pajak item.
      
    - Relasi :
      
      Berhubungan dengan Item dalam relasi many-to-one (banyak rincian pesanan dapat memiliki item yang sama).
      
    - Metode
      
      calcSubTotal(): Menghitung subtotal untuk item berdasarkan jumlahnya.
      
      calcWeight(): Menghitung berat total item.
      
      calcTax(): Menghitung pajak untuk item.
      
- Class Item
  ```
  public class Item {
    private double shippingWeight;
    private String description;

    public double getShippingWeight() {
        return shippingWeight;
    }

    public void setShippingWeight(double shippingWeight) {
        this.shippingWeight = shippingWeight;
    }

    public String getDescription() {
        return description;
    }

    public void setDescription(String description) {
        this.description = description;
    }

    public double getPriceForQuantity(int quantity) {
        return quantity * 100; // Harga per barang (contoh statis)
    }

    public double getTax() {
        return 10; // Pajak (contoh statis)
    }

    public boolean inStock() {
        return true; // Selalu tersedia untuk contoh
    }
  }
  ```
  - Kelas ini merepresentasikan rincian setiap item dalam sebuah pesanan, dengan atribut:
    
    shippingWeight: Berat barang.
    
    description: Deskripsi barang.
    
  - Metode :
    
    getPriceForQuantity(): Mengembalikan harga barang untuk jumlah tertentu.
    
    getTax(): Mengembalikan pajak untuk barang.
    
    inStock(): Mengecek ketersediaan barang.
    
- Class Payment
  ```
  public abstract class Payment {
    private float amount;

    public float getAmount() {
        return amount;
    }

    public void setAmount(float amount) {
        this.amount = amount;
    }

    public abstract boolean authorized();
  }
  ```
  - Kelas abstrak yang merepresentasikan pembayaran, memiliki atribut:

    amount: Jumlah pembayaran.
    
  - Relasi :

    Berhubungan dengan Order dalam relasi one-to-many (1 pesanan bisa memiliki beberapa metode pembayaran).
    
  - Metode :
    
    authorized(): Metode abstrak untuk mengecek otorisasi pembayaran.
    
- Class Cash
  ```
  public class Cash extends Payment {
    private float cashTendered;

    public float getCashTendered() {
        return cashTendered;
    }

    public void setCashTendered(float cashTendered) {
        this.cashTendered = cashTendered;
    }

    @Override
    public boolean authorized() {
        return cashTendered >= getAmount();
    }
  }
  ```
  - Subclass dari Payment yang merepresentasikan pembayaran dengan uang tunai. Memiliki atribut tambahan:

    cashTendered: Jumlah uang tunai yang diberikan.
    
  - Metode :

    authorized(): Mengecek apakah uang tunai yang diberikan cukup untuk membayar pesanan.
    
- Class Check
  ```
  public class Check extends Payment {
    private String name;
    private String bankID;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getBankID() {
        return bankID;
    }

    public void setBankID(String bankID) {
        this.bankID = bankID;
    }

    @Override
    public boolean authorized() {
        return bankID != null && !bankID.isEmpty();
    }
  }
  ```
  - Subclass dari Payment yang merepresentasikan pembayaran dengan cek. Memiliki atribut tambahan:

    name: Nama pemilik cek.

    bankID: ID bank yang mengeluarkan cek.
    
  - Metode :
    
    authorized(): Mengecek apakah cek valid (dalam implementasi sederhana, selalu diotorisasi).
    
- Class Credit
  ```
  public class Credit extends Payment {
    private String number;
    private String type;
    private String expDate;

    public String getNumber() {
        return number;
    }

    public void setNumber(String number) {
        this.number = number;
    }

    public String getType() {
        return type;
    }

    public void setType(String type) {
        this.type = type;
    }

    public String getExpDate() {
        return expDate;
    }

    public void setExpDate(String expDate) {
        this.expDate = expDate;
    }

    @Override
    public boolean authorized() {
        return number != null && !number.isEmpty() && expDate != null && !expDate.isEmpty();
    }
  }
  ```
  - Subclass dari Payment yang merepresentasikan pembayaran dengan kartu kredit. Memiliki atribut tambahan:

    number: Nomor kartu kredit.

    type: Jenis kartu kredit (misalnya Visa, MasterCard).

    expDate: Tanggal kedaluwarsa kartu kredit.
    
  - Metode :
  - 
    authorized(): Mengecek otorisasi kartu kredit (dalam implementasi sederhana, selalu diotorisasi).
    
- Class Main
  ```
  import java.util.ArrayList;

  public class Main {
    public static void main(String[] args) {
        // Membuat customer
        Customerr customer = new Customerr();
        customer.setName("John Doe");
        customer.setAddress("123 Main Street");

        // Membuat item
        Item item1 = new Item();
        item1.setDescription("Laptop");
        item1.setShippingWeight(5.0);

        // Membuat detail order
        OrderDetail detail1 = new OrderDetail();
        detail1.setQuantity(2);
        detail1.setTaxStatus("Taxable");
        detail1.setItem(item1);

        // Membuat pesanan (order)
        Order order1 = new Order();
        order1.setDate("2024-12-04");
        order1.setStatus("Processing");
        order1.addOrderDetail(detail1);

        // Menambahkan order ke customer
        customer.addOrder(order1);

        // Membuat pembayaran dengan tunai
        Cash cashPayment = new Cash();
        cashPayment.setAmount(1000.0f); // Total pembayaran
        cashPayment.setCashTendered(1200.0f); // Uang yang diterima
        order1.addPayment(cashPayment);

        // Membuat pembayaran dengan kartu kredit
        Credit creditPayment = new Credit();
        creditPayment.setAmount(500.0f);
        creditPayment.setNumber("1234-5678-9012-3456");
        creditPayment.setType("Visa");
        creditPayment.setExpDate("12/2025");
        order1.addPayment(creditPayment);

        // Output informasi customer
        System.out.println("Customer Name: " + customer.getName());
        System.out.println("Customer Address: " + customer.getAddress());

        // Output informasi pesanan
        System.out.println("\nOrder Date: " + order1.getDate());
        System.out.println("Order Status: " + order1.getStatus());
        System.out.println("Item Description: " + detail1.getItem().getDescription());
        System.out.println("Item Quantity: " + detail1.getQuantity());
        System.out.println("Order Total: $" + order1.calcTotal());
        System.out.println("Order Weight: " + order1.calcWeight() + " kg");

        // Output pembayaran
        for (Payment payment : order1.getPayments()) {
            System.out.println("\nPayment Amount: $" + payment.getAmount());
            System.out.println("Payment Authorized: " + payment.authorized());
            switch (payment) {
                case Cash cash -> System.out.println("Cash Tendered: $" + cash.getCashTendered());
                case Credit credit -> {
                    System.out.println("Credit Card Number: " + credit.getNumber());
                    System.out.println("Credit Card Type: " + credit.getType());
                    System.out.println("Credit Card Expiry: " + credit.getExpDate());
                }
                default -> {
                }
            }
        }
    }
    }
    ```
# Output
![Screenshot 2024-12-04 214535](https://github.com/user-attachments/assets/b50f28d7-accd-4796-9901-926855907f8d)
