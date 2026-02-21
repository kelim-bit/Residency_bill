# Integração Firebase (Auth + Firestore) — Segurança

## 1) Configuração obrigatória
1. No arquivo `gastos_residencia.html`, preencher `FIREBASE_CONFIG` com os dados do projeto.
2. Em **Authentication**, habilitar `Email/Password`.
3. Em **Firestore Database**, criar em modo bloqueado e aplicar regras abaixo.

## 2) Regras Firestore (mínimo seguro)
```rules
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users_finance/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
    match /{document=**} {
      allow read, write: if false;
    }
  }
}
