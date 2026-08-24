# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-24T18:50:01.922305+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×21 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×76 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×21 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-24T18:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×45  [2026-08-24T18:05:44]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×45  [2026-08-24T18:05:44]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×45  [2026-08-24T18:05:44]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×48  [2026-08-24T18:02:30]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×19  [2026-08-24T17:51:39]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-08-24T14:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×21  [2026-08-24T10:04:46]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ORPHAN_SCAN  ×1  [2026-08-24T06:00:18]
- key: `ORPHAN_SCAN|192 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-24T06:00:18]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-24T06:00:18]
- key: `INSUFFICIENT_SAMPLE|S00: n=164<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-24T06:00:18]
- key: `ROI_STAT|S00: n=164 hit%=26.8% hit_CI[Bonf]=[18.1,37.8]% ROI=0.82 ROI_boot95=[0.56,1.10]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-24T06:00:18]
- key: `ROI_STAT|S01_NAKAANA1: n=186 hit%=25.8% hit_CI[Bonf]=[17.7,36.0]% ROI=0.83 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-24T06:00:18]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=186<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-24T06:00:18]
- key: `ROI_STAT|S02_TETSUBAN: n=80 hit%=42.5% hit_CI[Bonf]=[28.0,58.4]% ROI=0.68 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-24T06:00:18]
- key: `DRIFT_BUCKET|drift ≤-30%: n=36 hit%=19.4% ROI=0.62 (コスト 10,400/回収 6,410)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-24T06:00:18]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=38 hit%=36.8% ROI=0.99 (コスト 8,800/回収 8,710)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-24T06:00:18]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=91 hit%=29.7% ROI=0.91 (コスト 21,000/回収 19,070)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-24T06:00:18]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=53 hit%=24.5% ROI=0.51 (コスト 12,100/回収 6,180)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-24T06:00:18]
- key: `DRIFT_BUCKET|drift ≥+30%: n=37 hit%=21.6% ROI=0.98 (コスト 10,100/回収 9,940)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 11.38MB / last modified 2026-08-24T18:49:30.784604+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
t=5000
2026-08-24 18:48:03,672 [INFO] predictor: Models loaded OK
2026-08-24 18:48:16,105 [INFO] scraper: odds3t: 120/120 parsed
2026-08-24 18:48:17,244 [INFO] scraper: odds3f: 20/20 parsed
2026-08-24 18:48:18,365 [INFO] scraper: odds2t: 30/30 parsed
2026-08-24 18:48:18,366 [INFO] scraper: odds2f: 14/15 parsed
2026-08-24 18:48:19,460 [INFO] scraper: odds_win: 4/6 parsed
2026-08-24 18:48:19,460 [INFO] scraper: fetch_race 15/9: boats=6 odds=188/191
2026-08-24 18:48:19,463 [INFO] predictor: CALIBRATION_MODE=on
2026-08-24 18:48:19,464 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-08-24 18:48:19,468 [INFO] run_cycle: fetched 15/9 [scan]: 154 combos
2026-08-24 18:48:19,569 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-24 18:49:03,433 [INFO] run_cycle: === run_cycle 18:49:03 ===
2026-08-24 18:49:03,433 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-24 18:49:03,433 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-24 18:49:03,479 [INFO] predictor: Models loaded OK
2026-08-24 18:49:14,723 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=9&jcd=07&hd=20260824: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-08-24 18:49:27,086 [INFO] scraper: odds3t: 120/120 parsed
2026-08-24 18:49:28,175 [INFO] scraper: odds3f: 20/20 parsed
2026-08-24 18:49:29,280 [INFO] scraper: odds2t: 30/30 parsed
2026-08-24 18:49:29,281 [INFO] scraper: odds2f: 15/15 parsed
2026-08-24 18:49:30,377 [INFO] scraper: odds_win: 6/6 parsed
2026-08-24 18:49:30,377 [INFO] scraper: fetch_race 07/9: boats=6 odds=191/191
2026-08-24 18:49:30,381 [INFO] predictor: CALIBRATION_MODE=on
2026-08-24 18:49:30,381 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-24 18:49:30,385 [INFO] run_cycle: fetched 07/9 [scan]: 156 combos
2026-08-24 18:49:30,510 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 76
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 76
  }
]
```

## Phase別通知記録 (24h)
{'final': 32, 'result': 11, 'scan': 33}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 194
  FINAL_MISSING: 76
  CIRCUIT_BREAKER_TRIP: 21
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 9
  ANOMALY_SCAN_FINAL_RATIO: 5
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 16 | 12,600 | 18,150 | +5,550 | 1.44 |
| S01_NAKAANA1 | 51 | 18 | 10,200 | 11,680 | +1,480 | 1.145 |
| S02_TETSUBAN | 20 | 6 | 4,000 | 2,380 | -1,620 | 0.595 |

## 直近アラート (24h・新しい順)
```
[18:47:04] FINAL_MISSING: {"deadline": "2026-08-24T15:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082422071514", "sid": "S00"}
[18:29:25] FINAL_MISSING: {"deadline": "2026-08-24T10:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082418061055", "sid": "S01_NAKAANA1"}
[18:29:25] FINAL_MISSING: {"deadline": "2026-08-24T10:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082418061055", "sid": "S00"}
[18:20:05] CIRCUIT_BREAKER_TRIP: {"cost": 4000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 20, "payout": 2380, "roi_7d": 0.595, "sid": "S02_TETSUBAN"}
[18:15:26] FINAL_MISSING: {"deadline": "2026-08-24T13:42:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082418111342", "sid": "S00"}
[18:09:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 815}
[18:08:37] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[18:08:37] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[18:08:37] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 806}
[18:07:04] FINAL_MISSING: {"deadline": "2026-08-24T17:37:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082407061737", "sid": "S00"}
```

## 本日残レース: 16件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 128件 締切済
- 通知発射: scan=25 nid / final=25 nid / result=9 nid
- predictions: 9 / うち結果DB記録済: 9
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 6件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 206R | win | 1 | 0.4111 | 3.7 | 1.52 | 200 | scan=- drift=- | 17:41:18 |
| S00 | 074R | win | 1 | 0.1084 | 4.1 | 0.44 | 300 | scan=7.8 drift=-47.4% | 16:36:19 |
| S00 | 1310R | win | 1 | 0.5476 | 6.4 | 3.50 | 300 | scan=- drift=- | 15:04:31 |
| S01_NAKAANA1 | 036R | win | 1 | 0.5123 | 3.9 | 2.00 | 200 | scan=4.7 drift=-17.0% | 13:26:19 |
| S01_NAKAANA1 | 1010R | win | 1 | 0.5174 | 3.1 | 1.60 | 200 | scan=- drift=- | 13:10:23 |
| S01_NAKAANA1 | 109R | win | 1 | 0.5174 | 4.0 | 2.07 | 200 | scan=4.6 drift=-13.0% | 12:37:27 |
| S01_NAKAANA1 | 188R | win | 1 | 0.4111 | 3.7 | 1.52 | 200 | scan=- drift=- | 11:57:19 |
| S00 | 134R | win | 1 | 0.3177 | 5.5 | 1.75 | 300 | scan=9.7 drift=-43.3% | 11:48:19 |
| S00 | 082R | win | 1 | 0.4111 | 7.0 | 2.88 | 300 | scan=15.7 drift=-55.4% | 10:56:32 |
| S01_NAKAANA1 | 249R | win | 1 | 0.3177 | 3.9 | 1.24 | 200 | scan=4.0 drift=-2.5% | 21:22:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 63 | +6.8% | -79.6% | +320.7% | 24 | 10 | 45 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 524.1s |
| **Latency** (scan→final max) | 673.1s |
| **Traffic** (notifications 24h) | 76 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 1,000円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 427 | 0.4711 | 0.2974 | +0.1736 | 🟡+37% | 0.2391 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 162 | 0.4202 | 0.2654 | 0.2226 | 🔴-0.14 | 0.819 |
| S01_NAKAANA1 | win | 187 | 0.4886 | 0.2727 | 0.2482 | 🔴-0.25 | 0.851 |
| S02_TETSUBAN | win | 78 | 0.5347 | 0.4231 | 0.2512 | 🔴-0.03 | 0.672 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 10 | 0.1249 | 0.1000 | ✅+0.0249 |
| 0.15-0.20 | 9 | 0.1799 | 0.2222 | ✅-0.0423 |
| 0.20-0.30 | 9 | 0.2251 | 0.3333 | 🔴-0.1082 |
| 0.30-0.50 | 154 | 0.4113 | 0.2273 | 🔴+0.1841 |
| 0.50+ | 244 | 0.5444 | 0.3525 | 🔴+0.1919 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 118 | 0.77 |
| win | <5.0 | ✅learned | 218 | 0.748 |
| win | <10.0 | ✅learned | 103 | 0.453 |
| win | <20.0 | ✅learned | 30 | 0.227 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-08-24T18:50:01.922305+09:00_