# Lina Yönetim Paneli kurulumu

Bu geliştirme `feature/admin-panel` dalındadır. Mevcut `main` sitesi değiştirilmedi.

## 1. Supabase
1. https://supabase.com/dashboard adresinden yeni proje oluşturun.
2. SQL Editor > New query > `supabase-schema.sql` içeriğini çalıştırın.
3. Authentication > Users > Add user bölümünden kendi yönetici e-postanızı ve güçlü şifrenizi oluşturun.
4. Oluşturulan kullanıcının UUID'sini kopyalayın. SQL Editor'de şu sorguyu çalıştırın:
   `insert into public.lina_admins(user_id) values ('BURAYA_USER_UUID');`
5. Project Settings / API Keys bölümünden Project URL ve publishable (veya anon) key alın.
6. `lina-config.js` içine bunları girin. **Secret/service_role key asla eklemeyin.**

## 2. Yayın
`feature/admin-panel` dalını Vercel Preview olarak test edin; her şey çalışınca main'e birleştirin. `/admin.html` yönetici girişi, ana sayfa ise herkese açık sitedir.

## 3. İşlevler
- Giriş yalnızca `lina_admins` tablosundaki kullanıcılara açıktır.
- Site başlığı, açıklamalar, WhatsApp numarası güncellenebilir.
- Hizmetler eklenir, düzenlenir, silinir.
- Fotoğraflar Supabase Storage'a yüklenir, galeriye yansır, silinir.
- Maksimum 10 MB JPG/PNG/WebP.
- Supabase URL/anahtarları olmadan panel işlevleri çalışmaz.

## Güvenlik
- RLS tüm tablolarda etkin.
- Görseller herkese açık bucket içinde saklanır; müşteri özel/kişisel görselleri yüklemeyin.
- Yönetici yetkisi sadece SQL ile tanımlanır, tarayıcıdan verilemez.
