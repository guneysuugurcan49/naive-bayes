Twitter Duygu Analizi Projesi
Genel Bakış
Bu proje, Twitter verileri üzerinde duygu analizi yapmak için bir makine öğrenimi modeli geliştirmeyi amaçlamaktadır. Proje, veri setinin yüklenmesi, temizlenmesi, özellik çıkarımı, model eğitimi ve değerlendirmesini kapsamaktadır.

Kullanılan Kütüphaneler
Projede kullanılan başlıca kütüphaneler şunlardır:

pandas: Veri manipülasyonu ve analizi için.
numpy: Sayısal işlemler için.
matplotlib ve seaborn: Veri görselleştirme için.
wordcloud: Kelime bulutu oluşturmak için.
scikit-learn: Makine öğrenimi modellemesi için (CountVectorizer, MultinomialNB, train_test_split, classification_report, confusion_matrix, accuracy_score, cross_val_score).
nltk: Doğal dil işleme görevleri için (stopwords, PorterStemmer).
zipfile ve os: Dosya işlemleri için.
re: Metin temizleme için düzenli ifadeler.
Veri Seti
Projede kullanılan veri seti, Twitter gönderilerinden oluşmaktadır. Veri seti training.1600000.processed.noemoticon.csv adlı bir CSV dosyasıdır ve sıkıştırılmış (archive.zip) olarak yüklenmiştir.

Veri seti aşağıdaki sütunları içermektedir:

target: Duygu etiketi (0: Negatif, 4: Pozitif).
ids: Tweet ID'si.
date: Tweet tarihi.
flag: Sorgu.
user: Kullanıcı adı.
text: Tweet içeriği.
Proje Adımları
Ortam Kurulumu ve Kütüphanelerin Yüklenmesi: Google Drive bağlandı ve gerekli kütüphaneler (wordcloud, nltk vb.) yüklendi. NLTK'nin stopwords verisi indirildi.
Veri Setinin Yüklenmesi ve Çıkarılması: archive.zip dosyası yüklenerek içeriği twitter_data klasörüne çıkarıldı.
Veri Setinin Okunması ve Hazırlanması: Çıkarılan CSV dosyası farklı kodlamalar denenerek okundu. Sütun isimleri belirlendi (target, ids, date, flag, user, text) ve sadece text ile target sütunları seçilerek sütun isimleri text ve label olarak değiştirildi.
Metin Temizleme: Tweet metinleri için temizleme fonksiyonları uygulandı. Bu fonksiyonlar muhtemelen küçük harfe çevirme, noktalama işaretlerini kaldırma, URL'leri kaldırma, stop words (durdurma kelimeleri) kaldırma ve kök bulma (stemming) işlemlerini içermektedir (Not: Notebook'ta clean_text, remove_stopwords ve apply_stemming fonksiyonlarının tanımları yer almamaktadır, ancak kullanıldıkları görülmektedir). Temizlenmiş metinler cleaned_text sütununa kaydedildi.
Özellik Çıkarımı: Temizlenmiş metinler CountVectorizer kullanılarak sayısal vektörlere dönüştürüldü (Bag-of-Words modeli). text sütunu özellik (X), label sütunu ise hedef değişken (y) olarak belirlendi.
Veri Bölme: Veri seti, eğitim (%80) ve test (%20) kümelerine ayrıldı.
Model Eğitimi: Multinomial Naive Bayes modeli eğitim verisi (X_train, y_train) üzerinde eğitildi.
Model Değerlendirmesi:
Eğitim ve test setleri üzerinde modelin doğruluk oranı (accuracy) hesaplandı.
Detaylı bir sınıflandırma raporu (classification_report) oluşturularak precision, recall ve f1-score metrikleri incelendi.
Modelin performansını görselleştirmek için bir karışıklık matrisi (confusion_matrix) çizildi.
Örnek bir metin üzerinde tahmin yapıldı ve tahmin olasılıkları görüntülendi.
Modelin genelleme performansını değerlendirmek için 5 katlı çapraz doğrulama (cross_val_score) yapıldı ve ortalama doğruluk oranı ile standart sapması hesaplandı.
Modelin belirlediği en önemli pozitif ve negatif kelimeler listelendi.
Sonuçlar
Model, eğitim setinde %80.05 ve test setinde %76.64 doğruluk oranı elde etmiştir. Çapraz doğrulama sonuçları da benzer bir ortalama doğruluk oranı (%75.99) göstermektedir. Karışıklık matrisi ve sınıflandırma raporu, modelin her iki sınıf (negatif ve pozitif) için de makul bir performans sergilediğini göstermektedir. En önemli kelimelerin analizi, modelin hangi kelimeleri pozitif veya negatif duygu ile ilişkilendirdiğini anlamamıza yardımcı olmuştur.

Gelecekteki İyileştirmeler
Daha gelişmiş metin ön işleme teknikleri (örneğin, lemmatization).
Farklı özellik çıkarım yöntemleri (örneğin, TF-IDF, Word Embeddings).
Diğer sınıflandırma algoritmalarının denenmesi (örneğin, SVM, Logistic Regression, Derin Öğrenme modelleri).
Hiperparametre optimizasyonu.
Daha büyük veya farklı veri setleri üzerinde eğitim.
