## Java OOP Concepts - Extended Detailed Answers

---

### 1. Why we need to use OOP? Some major OOP languages?

**Cevap:**  
OOP’nin temel amacı **gerçek dünya problemlerini, gerçek dünya nesneleri ile modellemek**. Yazılım geliştirmede kod tekrarını engeller, modülerliği artırır, karmaşıklığı gizler.  
**Faydalı OOP İlkeleri:**
- **Abstraction:** Gereksiz detayları gizleme.
- **Encapsulation:** Veri gizleme (private field + getter/setter).
- **Inheritance:** Mevcut özellikleri alt sınıflara miras verip kod tekrarını azaltma.
- **Polymorphism:** Aynı method isminin farklı şekillerde çalışabilmesi.

**Major OOP Languages:**
- **Java:** 
- **C++:** 
- **C#:** 
- **Python:** 
- **Ruby:** 

**Stack Overflow Insight:**  
OOP’nin en çok tartışıldığı konular: SOLID principles, design patterns (Factory, Singleton, Observer), ve real-world use-cases.

---

### 2. Interface vs Abstract Class?

**Cevap:**

| Özellik | Interface | Abstract Class |
|--------|---------|--------------|
| İçerik | Method imzaları, Java 8+ default/static methodlar | Hem abstract hem concrete methodlar içerir |
| Field | public, static, final | normal, static, final olabilir |
| Çoklu Kalıtım | Evet | Hayır |
| Constructor | Yok | Var |
| Kullanım Amacı | Farklı sınıflara aynı davranış | Temel sınıf davranışı tanımlama |
| Ne zaman kullanılır? | Bağımsız davranış tanımlamak için | Ortak base kod varsa |

**Stack Overflow Insight:**  
Interface’lerin çoklu kalıtım avantajı, abstract class’ların code reuse avantajıyla sık sık kıyaslanıyor. Özellikle Dependency Injection örneklerinde interface kullanımı öneriliyor.

---

### 3. Why we need equals and hashCode? When to override?

**Cevap:**  
Java’daki default `equals()` referans bazlıdır. Fakat içerik bazlı kıyas yapmak istediğimizde override gerekir.

**Neden override edilmeli?**
- Koleksiyonlar (HashSet, HashMap) nesneyi kıyaslarken hashCode kullanır.
- İki nesne eşitse, hashCode değerleri aynı olmalı (**Contract**).

**Ne zaman override?**
- Domain class'larda (örneğin: `Person`, `Product`) içerik eşitliği kontrol edilirken.

**Kod Örneği:**

```java
@Override
public boolean equals(Object obj) { /* id, name karşılaştırması */ }

@Override
public int hashCode() { return Objects.hash(id, name); }
```

**Stack Overflow Insight:**  
Hash collisions ve equals-hashCode uyumsuzluğu Java’da en sık hatalardan biri olarak tartışılıyor.

---

### 4. Diamond problem in Java? How to fix it?

**Cevap:**  
Java’da **class bazlı çoklu kalıtım yok**, bu yüzden diamond problem yok.

**Interface tarafında:**
İki interface aynı default method'u sağlarsa, implement eden sınıfta belirsizlik oluşur.

**Çözüm:**

```java
interface A { default void show() { System.out.println("A"); } }
interface B { default void show() { System.out.println("B"); } }
class C implements A, B {
    public void show() { A.super.show(); } // Çözüm burada
}
```

**Stack Overflow Insight:**  
Diamond problem çözümü, özellikle default methods sonrası Java 8 ile yeniden tartışılmış.

---

### 5. Why we need Garbage Collector? How does it run?

**Cevap:**

**Neden Lazım:**
- Manüel memory management hatalarına karşı JVM kontrol sağlar.
- Kullanılmayan nesneleri temizler.
  
**Nasıl Çalışır:**
1. **Mark and Sweep Algorithm:** Kullanılmayan nesneleri işaretleyip temizler.
2. **Generational GC:** Short-lived & long-lived nesneleri ayrı takip eder.
3. **Stop-the-World Event:** GC çalışırken uygulama durur.

**GC Türleri:**
- **Serial GC**
- **Parallel GC**
- **G1 GC**

**Stack Overflow Insight:**  
G1 GC tuning, Stop-the-World minimizasyonu en popüler konular arasında.

---

### 6. Java 'static' keyword usage?

**Cevap:**

**static** anahtar kelimesi, sınıf seviyesindeki üyeleri tanımlar. Nesneye değil, doğrudan sınıfa bağlıdır.

**Kullanım Alanları:**

- **Static Variable:** Tüm nesneler için ortaktır. Örnek: Sayaç.
- **Static Method:** Nesne oluşturmadan çağrılır. Örnek: `Math.max()`.
- **Static Block:** Class yüklenirken bir defa çalışır.
- **Static Nested Class:** Outer class instance’ına ihtiyaç duymadan çalışır.

**Stack Overflow Insight:**  
Static context'te instance variable kullanımı hatası, en yaygın sorulardan biri.

---

### 7. Immutability means? Where, How and Why to use it?

**Cevap:**

**Immutability:** Nesnenin state’i oluşturulduktan sonra değiştirilemez.

**Nerede Kullanılır:**
- **String** (Java’nın en bilinen immutable sınıfı)
- **Wrapper sınıflar** (Integer, Double)
- **Custom immutable class** (Final class, private final fields, setter yok)

**Neden:**
- Thread-safe (senkronizasyona gerek yok)
- Predictability (beklenmedik değişiklik olmaz)
- Hash-based yapılar için güvenli

**Nasıl Yapılır:**

```java
final class Person {
  private final String name;
  public Person(String name) { this.name = name; }
  public String getName() { return name; }
}
```

**GeeksforGeeks Insight:**  
Immutable sınıfların design pattern’lerde (Builder, Singleton) kullanımı çok yaygın.

---

### 8. Composition and Aggregation means and differences?

**Cevap:**

| Özellik | Composition | Aggregation |
|--------|------------|-------------|
| İlişki | Strong "Has-A" | Weak "Has-A" |
| Yaşam Döngüsü | Parent silinince child da silinir | Child bağımsız yaşar |
| Örnek | Car - Engine | Team - Player |

**Örnek Kod:**

```java
// Composition
class Engine { }
class Car { private Engine engine = new Engine(); }

// Aggregation
class Player { }
class Team { private List<Player> players; }
```

**Stack Overflow Insight:**  
Design decisions kısmında Aggregation mı Composition mı kullanılmalı sorusu sık tartışılıyor.

---

### 9. Cohesion and Coupling means and differences?

**Cevap:**

- **Cohesion (Uyumluluk):** Sınıf içindeki methodların birbiriyle alakasının derecesi.
  - **High Cohesion:** Tek sorumluluk, okunabilir.
  - **Low Cohesion:** Dağınık sorumluluklar, karmaşıklık.

- **Coupling (Bağlılık):** Sınıfların birbirine bağımlılık derecesi.
  - **Low Coupling:** Esnek, bağımsız sistemler.
  - **High Coupling:** Değişime kapalı, bağımlı sistemler.

**GeeksforGeeks Insight:**  
SOLID prensiplerinde özellikle Liskov ve Dependency Inversion’da bu kavramlar vurgulanıyor.

---

### 10. Heap and Stack means and differences?

| Özellik | Stack | Heap |
|--------|------|------|
| Ne Tutar? | Primitive değişkenler, method çağrıları | Nesneler, instance değişkenler |
| Yaşam Süresi | Method bitince biter | GC tarafından yönetilir |
| Hız | Çok hızlı | Görece yavaş |
| Memory Boyutu | Küçük | Büyük |

**Stack Overflow Insight:**  
Java'da OutOfMemoryError’ların çoğu Heap ile ilgilidir, StackOverflowError ise recursive methodlardan kaynaklanır.

---

### 11. Exception means? Type of Exceptions?

**Cevap:**

**Exception:** Program akışını bozan durumlar.

**Türleri:**
1. **Checked Exceptions:** Derleyici tarafından kontrol edilir. Örnek: `IOException`.
2. **Unchecked Exceptions:** Runtime’da oluşur. Örnek: `NullPointerException`.
3. **Errors:** JVM seviyesinde ciddi hatalar. Örnek: `OutOfMemoryError`.

**Stack Overflow Insight:**  
Try-catch best practice'leri ve custom exception yazımı en çok tartışılan konulardan.

---

### 12. How to summarize 'clean code' as short as possible?

**Cevap:**

**Clean Code Özellikleri:**
- Anlamlı isimler
- Kısa, tek sorumluluklu methodlar
- DRY (Don’t Repeat Yourself) prensibi
- Yorum satırına gerek bırakmayacak açıklık
- Test edilebilirlik
- Okunabilirlik > Clever kod

**Stack Overflow Insight:**  
Robert C. Martin’in Clean Code kitabı sürekli referans gösteriliyor, özellikle SOLID ilkeleriyle ilişkilendiriliyor.

---

### 13. What is the method of hiding in Java?

**Cevap:**

Java’da **Method Hiding**, static methodların alt sınıfta aynı signature ile yeniden tanımlanması durumunda oluşur.

**Özellikler:**
- Compile time’da bağlanır.
- Runtime polymorphism olmaz.
- Referans tipi belirleyici.

**Örnek:**

```java
class Parent { static void display() { System.out.println("Parent"); } }
class Child extends Parent { static void display() { System.out.println("Child"); } }
Parent p = new Child();
p.display(); // Output: Parent
```

**Stack Overflow Insight:**  
Static vs Non-static method overriding konuları sıkça karıştırılıyor.

---

### 14. What is the difference between abstraction and polymorphism in Java?

| Kavram | Açıklama |
|-------|---------|
| **Abstraction** | Gereksiz detayları gizler. Kullanıcıya sade API sunar. (abstract class & interface) |
| **Polymorphism** | Aynı method isminin farklı şekillerde çalışması. (Method Overriding & Overloading) |

**Örnek:**

```java
abstract class Animal { abstract void sound(); }
class Dog extends Animal { void sound() { System.out.println("Bark"); } }
class Cat extends Animal { void sound() { System.out.println("Meow"); } }
```

**Stack Overflow Insight:**  
Run-time polymorphism (dynamic dispatch) Java interview’lerinde en çok sorulan konulardan biri.

---
