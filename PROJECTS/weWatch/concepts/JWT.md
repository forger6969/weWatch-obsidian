---
type: concept
tags: [security, auth, weWatch]
---
# 🔑 JWT

**Hub:** [[../00-weWatch-Overview]] | **Service:** [[../services/auth]]

## Схема
- Access token: 15min, RS256, payload: {userId, email, role, username}
- Refresh token: 30d, MongoDB, hashed

## Middleware
- verifyToken → req.user
- optionalAuth → public endpoints
- requireRole(role) → admin/operator
