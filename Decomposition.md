Decomposition

-Ne?
    Decomposition büyük bir problemi daha yönetilebilir alt problemlere ayırma sürecidir.

-Neden?

    Decomposition'un amacı problemi bağımsız alt problemlere bölerek basit, daha yönetilebilir ve anlaşılabilir bir kod yazmaktır.
Bir böl ve yönet stratejisi de denilebilir. Alt bölümler bağımsız ve dışarıdan bakıldığında bu sayede daha anlaşılabilir olur.
Örnek vermek gerekirse İki adet 500 satırlık program yazmak, 1000 satırlık bir program yazmaktan çok daha kolaydır.
Bunun yanı sıra kodu tekrar gözden geçirecek kişi için de büyük kolaylık sağlamış olur.


-Nasıl?

    C# veya Java gibi nesneye yönelimi destekleyen dillerde Decomposition sınıflar üzerinden yapılır.
Ayrıştırmanın işe yaraması için, tüm problemin alt bölümlerinin mümkün olduğunca birbirinden bağımsız olması gerekir.
Bu onların alt bölümlerinin olmayacağı anlamına gelmez, tamamen birbirine bağlıdır.
Sadece gereksiz yere birbirlerinin detaylarına bağlı kalmamalılar.

