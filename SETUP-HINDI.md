# VedraInvoice Phase 2 — आसान हिंदी सेटअप

यह ZIP पूरा source project है। Public link पाने के लिए इसे आपके hosting और Supabase accounts से connect करना होगा। ZIP अकेले अपने आप live नहीं होता, क्योंकि database URL/key आपके अपने account से आएंगे।

## A. Supabase database तैयार करें
1. https://supabase.com/ पर account बनाकर New project बनाएं।
2. Project dashboard में **SQL Editor** खोलें।
3. इस ZIP के `supabase/schema.sql` की पूरी file खोलकर copy करें, SQL Editor में paste करें और **Run** दबाएं। इससे customers, products, invoices और settings tables बनेंगी और Row Level Security policies भी लगेंगी।
4. Project Settings / API (या Connect) में Project URL और publishable/anon public key copy करें। **service_role key कभी भी frontend में न डालें।**

## B. Project को configure करें
1. ZIP extract करें।
2. `.env.example` की copy बनाकर उसका नाम `.env` रखें।
3. `.env` में अपने Supabase values भरें:

```
VITE_SUPABASE_URL=https://आपका-project.supabase.co
VITE_SUPABASE_ANON_KEY=आपकी-publishable-या-anon-public-key
```

4. कंप्यूटर पर Node.js 18 या नया install हो। Project folder में terminal खोलकर चलाएं:

```
npm install
npm run dev
```

5. Terminal जो local URL बताए, उसे browser में खोलें। Signup करके account बनाएं। Supabase email confirmation चालू हो तो inbox से confirm करें।

## C. Live link बनाएं (Netlify)
1. Project की सभी files GitHub repository में upload करें। `.env` upload न करें।
2. https://www.netlify.com/ पर GitHub repository import करें।
3. Build command: `npm run build`
4. Publish directory: `dist`
5. Site settings → Environment variables में `VITE_SUPABASE_URL` और `VITE_SUPABASE_ANON_KEY` डालें।
6. Deploy करें। Netlify एक public URL देगा।
7. उस URL को Supabase Authentication → URL Configuration में Site URL / Redirect URLs के अंदर जोड़ें।

## इस version में
- Email/password signup और login
- Supabase cloud database में customers, products, invoices और business settings
- हर logged-in user के लिए RLS policies
- GST line calculations, CGST/SGST या IGST display
- Invoice PDF download, CSV export, JSON backup/restore
- Partial/full payment record, UPI payment QR (QR भुगतान collect या verify नहीं करता)
- Dashboard, reports, search, dark mode, responsive layout

## जरूरी सीमाएं
- यह GST return file नहीं करता और GST compliance की guarantee नहीं देता। वास्तविक उपयोग से पहले accountant से invoice format/tax treatment verify कराएं।
- UPI QR केवल payment app खोलने के लिए URI/QR बनाता है; payment status verify नहीं करता। कोई payment gateway जुड़ा नहीं है।
- Live deployment, SMTP email delivery, account recovery, domain और Supabase project setup आपके accounts में पूरे करने होंगे।
- Public launch से पहले security review, backups, privacy policy, terms, rate limits और cross-account access tests करें।
