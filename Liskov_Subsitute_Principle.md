Liskov Substitution Principle

-Ne?
    Kısaca tanımlamak gerekirse, alt sınıflardan oluşturulan nesneler üst sınıfların nesneleriyle yer değiştirdiklerinde aynı davranışı göstermek zorundadırlar.

-Neden?

    LSP’ye göre herhangi bir sınıf kullanıcısı, bu sınıfın alt sınıfları kullanmak için özel bir efor sarf etmek zorunda kalmamalıdır. Onun bakış açısından üst sınıf ve alt sınıf arasında farklılık yoktur. Üst sınıf nesnelerinin kullanıldığı metotlar içinde alt sınıftan olan nesneler aynı davranışı sergilemek zorundadır, çünkü oluşturulan metotlar üst sınıf davranışları örnek alınarak programlanmıştır. Alt sınıflarda meydana gelen davranış değişiklikleri, bu metotların hatalı çalışmasına sebep verebilir. Özellikte bu metotlarda instanceof gibi nesnelerin tipleri arasında kıyaslama yapılmak zorunda kalındığı zaman, LSP prensibi çiğnenmiş olur ki, bu alt sınıfların varlığından haberdar olunduğu anlamına gelir. Kullanıcı sınıflar ideal durumda alt sınıfların varlığından haberdar bile olmamalıdır.

-Nasıl?

    LSP’ye uymayan Kare ve dikdörtgen örneğiyle başlayalım.

    public class Square extends Rectangle {
    @Override
    public void setWidth(int width) {
        super.setWidth(width);
        super.setHeight(width);
    }
    @Override
    public void setHeight(int height) {
        super.setHeight(height);
        super.setWidth(height);
    }
}

Matematiksel olarak bir kareyi de bir dikdörtgen olarak kabul edebiliriz. Ama yazılım dünyasında da böyle kabul etmeli miydik ?

@Test
public void testRectangleArea() throws Exception {
    Rectangle rectangle = new Square();
    rectangle.setWidth(20);
    rectangle.setHeight(4);
    assertEquals(80, rectangle.area());
}

Kareyi de beklendiği yerde dikdörtgen olarak kullanılabilir hale getirmiş olduk. Ancak böyle yaparak dikdörtgen davranışındaki beklentiyi bozuyoruz. Çünkü karenin sadece tek bir kenar bilgisi yeterlidir yada uzunluk ve en bilgisi aynı olmak durumundadır.

Matematiksel olarak karenin dikdörtgenden türediğini varsayabiliriz. Ama davranışsal olarak Kare Dikdörtgenin yerine geçmez, bu hiyerarşi Liskov prensibini (LSP) ihlal eder.

O halde kareyi ve dikdörtgen’i LSP’ye prensibe uygun hale getirelim. Bu prensip, Open/Closed prensibine benzer ve open/closed prensibine uymak liskov prensibinin uygulanmasını kolaylaştırmaktadır.

Bir karenin yüksekliğinin / genişliğinin değiştirilmesi, bir dikdörtgenin yüksekliğinin / genişliğinin değiştirilmesinden daha farklı davranır. Her ikiside birer şekli temsil eder. Buradan yola çıkarak şekil interface’ini oluşturalım.

public interface Shape {
    long area();
}

Kare bir şekildir o halde Square adlı bir sınıf yaratarak Shape’den implement edebiliriz.

public class Square implements Shape {
private int size;
public Square(int size) {
        this.size = size;
    }
@Override
    public long area() {
        return size * size;
    }
public void setSize(int size) {
        this.size = size;
    }
}
Dikdörtgen Kare ile farklı davranışlar gösterebiliyor o halde onu ayrı bir şekil olarak Rectangle adlı bir sınıf yaratıp Shape’den implement edebiliriz.

public class Rectangle implements Shape {
    private int width;
    private int height;
    public Rectangle(int width, int height) {
        this.width = width;
        this.height = height;
    }
    @Override
    public long area() {
        return width * height;
    }
    public void setWidth(int width) {
        this.width = width;
    }
    public void setHeight(int height) {
        this.height = height;
    }
}

Artık Kare ve Dikdörtgen kendi davranışlarına sahip oldu. Ve her biri ayrı şekil olarak kabul ediliyor. Böylece alan hesaplama her bir şekile özgü matematiksel bir işlem içerebiliyor. Hadi test edelim.

    @Test
    public void testRectangleArea() throws Exception {
        Shape rectangle = new Rectangle(10, 5);
        assertEquals(50, rectangle.area());
    }
    @Test
    public void testSquareArea() throws Exception {
        Shape square = new Square(5);
        assertEquals(25, square.area());
    }


LSP’ye uygunluk tam olarak sınıflardan beklenen davranışları karşılayabilecek bir hiyerarşi düzeni oluşturarak sınıf yapılarımızı geliştirmektir.

