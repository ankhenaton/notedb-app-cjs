
# Notedb App (CJS) — Not Alma & Doküman Arşivi

Bu sürüm, geliştirmede yaşanan ESM/CJS uyumsuzluklarını gidermek için **CommonJS** derleme hedefi ile hazırlanmıştır ve kapsamlı **hata yakalama/handling** ekleri içerir.

## Öne Çıkanlar
- Kullanıcı bazlı izolasyon (JWT) ve bcrypt ile parola hash.
- Notlar: renk, sabitleme (pinned), drag&drop ile sıra, tarih-saatli hatırlatma.
- Doküman arşivi: dosya yükleme, kaynak URL, edinim tarihi, indirme, arama.
- Geliştirilmiş **error handling** ve **girdi doğrulama** (sunucu tarafı).
- CORS ve Helmet ile temel güvenlik sertleştirmeleri.

## Kurulum
### Backend
```bash
cd backend
cp .env.example .env
npm install
npx prisma migrate dev --name init
npm run dev        # geliştirme
# veya
npm run build && npm start
```

### Frontend
```bash
cd frontend
npm install
npm run dev        # http://localhost:5173
```

### Docker (opsiyonel)
```bash
docker compose up --build
```

### .env (backend)
```
PORT=4000
JWT_SECRET=degistir-bunu
CLIENT_ORIGIN=http://localhost:5173
NODE_ENV=development
```

## API (özet)
- **Auth**: `POST /api/auth/register` `{ username, password }`, `POST /api/auth/login`
- **Notes**: CRUD + `PATCH /api/notes/reorder`
- **Reminders**: `GET /api/reminders/due`, `POST /api/reminders/ack`
- **Documents**: `GET/POST /api/documents`, `GET /api/documents/:id/download`, `DELETE /api/documents/:id`

## Notlar
- Hatırlatmalar istemci çevrimiçi iken bildirim iletir (polling). Üretimde push/email eklenebilir.
- Dosyalar `backend/uploads/<userId>/` altında saklanır.
