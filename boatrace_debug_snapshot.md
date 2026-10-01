# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-01T14:50:01.391004+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×55 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×27 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×7 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×43  [2026-10-01T14:04:40]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×86  [2026-10-01T14:04:40]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×43  [2026-10-01T14:04:40]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-10-01T13:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-10-01T13:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×9  [2026-10-01T11:51:52]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🔴 SEND_WITHOUT_DBREC  ×1  [2026-10-01T11:25:50]
- key: `SEND_WITHOUT_DBREC|`
- **FIX**: record_notification の例外→DB書込エラー原因特定（WAL、ロック）

### 🟡 ANOMALY_BET_VOLUME_DROP  ×20  [2026-10-01T11:01:23]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×15  [2026-10-01T10:33:28]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-01T06:00:50]
- key: `INSUFFICIENT_SAMPLE|S00: n=167<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-01T06:00:50]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=79<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-01T06:00:50]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=163<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-01T06:00:50]
- key: `ORPHAN_SCAN|176 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-01T06:00:50]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=42 hit%=26.2% ROI=0.48 (コスト 9,300/回収 4,460)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-10-01T06:00:50]
- key: `ROI_STAT|S00: n=167 hit%=22.8% hit_CI[Bonf]=[14.8,33.3]% ROI=0.68 ROI_boot95=[0.45,0.94]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-01T06:00:50]
- key: `ROI_STAT|S01_NAKAANA1: n=163 hit%=23.9% hit_CI[Bonf]=[15.7,34.7]% ROI=0.74 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-01T06:00:50]
- key: `ROI_STAT|S02_TETSUBAN: n=79 hit%=48.1% hit_CI[Bonf]=[32.8,63.7]% ROI=0.81 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-01T06:00:50]
- key: `DRIFT_BUCKET|drift ≤-30%: n=29 hit%=37.9% ROI=1.16 (コスト 8,100/回収 9,360)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-01T06:00:50]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=42 hit%=26.2% ROI=0.70 (コスト 9,700/回収 6,790)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-01T06:00:50]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=96 hit%=24.0% ROI=0.72 (コスト 22,400/回収 16,180)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 14.69MB / last modified 2026-10-01T14:49:29.424720+09:00

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
 run_cycle 14:48:05 ===
2026-10-01 14:48:05,602 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-01 14:48:05,602 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-01 14:48:05,637 [INFO] predictor: Models loaded OK
2026-10-01 14:48:05,980 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-01 14:49:05,580 [INFO] run_cycle: === run_cycle 14:49:05 ===
2026-10-01 14:49:05,580 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-01 14:49:05,580 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-01 14:49:05,628 [INFO] predictor: Models loaded OK
2026-10-01 14:49:17,120 [INFO] scraper: odds3t: 120/120 parsed
2026-10-01 14:49:18,202 [INFO] scraper: odds3f: 20/20 parsed
2026-10-01 14:49:19,386 [INFO] scraper: odds2t: 30/30 parsed
2026-10-01 14:49:19,387 [INFO] scraper: odds2f: 15/15 parsed
2026-10-01 14:49:20,489 [INFO] scraper: odds_win: 6/6 parsed
2026-10-01 14:49:20,489 [INFO] scraper: fetch_race 03/9: boats=6 odds=191/191
2026-10-01 14:49:20,493 [INFO] predictor: CALIBRATION_MODE=on
2026-10-01 14:49:20,493 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-01 14:49:20,497 [INFO] run_cycle: fetched 03/9 [final]: 156 combos
2026-10-01 14:49:24,565 [INFO] scraper: odds3t: 120/120 parsed
2026-10-01 14:49:25,666 [INFO] scraper: odds3f: 20/20 parsed
2026-10-01 14:49:26,905 [INFO] scraper: odds2t: 30/30 parsed
2026-10-01 14:49:26,906 [INFO] scraper: odds2f: 15/15 parsed
2026-10-01 14:49:28,008 [INFO] scraper: odds_win: 4/6 parsed
2026-10-01 14:49:28,008 [INFO] scraper: fetch_race 13/10: boats=6 odds=189/191
2026-10-01 14:49:28,011 [INFO] predictor: CALIBRATION_MODE=on
2026-10-01 14:49:28,011 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-10-01 14:49:28,015 [INFO] run_cycle: fetched 13/10 [scan]: 154 combos
2026-10-01 14:49:28,331 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 88
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 88
  }
]
```

## Phase別通知記録 (24h)
{'final': 36, 'result': 19, 'scan': 33}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 76
  FINAL_MISSING: 55
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 27
  STRATEGY_CI_FAIL: 17
  PSI_DRIFT_DETECTED: 7
  ANOMALY_SCAN_FINAL_RATIO: 3
  ANOMALY_BET_VOLUME_DROP: 2
  ANOMALY_BET_VOLUME_SPIKE: 1
  CRITICAL_ODDS_COLLAPSE: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 9 | 12,600 | 6,750 | -5,850 | 0.536 |
| S01_NAKAANA1 | 44 | 14 | 8,800 | 8,480 | -320 | 0.964 |
| S02_TETSUBAN | 22 | 13 | 4,400 | 4,480 | +80 | 1.018 |

## 直近アラート (24h・新しい順)
```
[14:45:46] CIRCUIT_BREAKER_TRIP: {"cost": 12600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 42, "payout": 6750, "roi_7d": 0.536, "sid": "S00"}
[14:28:26] FINAL_MISSING: {"deadline": "2026-10-01T11:57:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100109041157", "sid": "S00"}
[14:26:31] FINAL_MISSING: {"deadline": "2026-10-01T13:56:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100103071356", "sid": "S00"}
[14:21:01] FINAL_MISSING: {"deadline": "2026-10-01T13:50:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100123111350", "sid": "S00"}
[14:04:39] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[14:04:39] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[14:04:39] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[14:00:53] FINAL_MISSING: {"deadline": "2026-10-01T09:27:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100114030927", "sid": "S00"}
[13:45:34] CIRCUIT_BREAKER_TRIP: {"cost": 12600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 42, "payout": 6750, "roi_7d": 0.536, "sid": "S00"}
[13:27:21] FINAL_MISSING: {"deadline": "2026-10-01T11:57:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100109041157", "sid": "S00"}
```

## 本日残レース: 86件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 82件 締切済
- 通知発射: scan=21 nid / final=22 nid / result=13 nid
- predictions: 13 / うち結果DB記録済: 13
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 5件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 138R | win | 1 | 0.5174 | 14.7 | 7.61 | 300 | scan=- drift=- | 13:45:20 |
| S02_TETSUBAN | 166R | win | 1 | 0.4989 | 2.1 | 1.05 | 200 | scan=- drift=- | 13:25:20 |
| S00 | 137R | win | 1 | 0.5123 | 9.1 | 4.66 | 300 | scan=11.5 drift=-20.9% | 13:19:21 |
| S00 | 065R | win | 1 | 0.5123 | 22.7 | 11.63 | 300 | scan=43.5 drift=-47.8% | 13:02:19 |
| S01_NAKAANA1 | 096R | win | 1 | 0.5735 | 3.5 | 2.01 | 200 | scan=- drift=- | 12:51:19 |
| S00 | 239R | win | 1 | 0.3177 | 8.2 | 2.61 | 300 | scan=7.1 drift=+15.5% | 12:36:21 |
| S01_NAKAANA1 | 043R | win | 1 | 0.5123 | 4.5 | 2.31 | 200 | scan=3.0 drift=+50.0% | 11:51:31 |
| S01_NAKAANA1 | 222R | win | 1 | 0.6037 | 4.1 | 2.48 | 200 | scan=3.1 drift=+32.3% | 11:42:20 |
| S00 | 133R | win | 1 | 0.5735 | 4.4 | 2.52 | 300 | scan=8.2 drift=-46.3% | 11:30:50 |
| S00 | 093R | win | 1 | 0.5174 | 4.5 | 2.33 | 300 | scan=- drift=- | 11:25:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 69 | +7.6% | -76.2% | +357.1% | 23 | 9 | 46 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 475.0s |
| **Latency** (scan→final max) | 623.8s |
| **Traffic** (notifications 24h) | 88 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,400円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 409 | 0.4786 | 0.2861 | +0.1926 | 🟡+40% | 0.2471 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 168 | 0.4469 | 0.2202 | 0.2451 | 🔴-0.43 | 0.653 |
| S01_NAKAANA1 | win | 160 | 0.4893 | 0.2562 | 0.2457 | 🔴-0.29 | 0.789 |
| S02_TETSUBAN | win | 81 | 0.5233 | 0.4815 | 0.2541 | 🔴-0.02 | 0.815 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0730 | 0.4000 | 🔴-0.3270 |
| 0.30-0.50 | 156 | 0.4161 | 0.2436 | 🔴+0.1725 |
| 0.50+ | 237 | 0.5434 | 0.3165 | 🔴+0.2270 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 165 | 0.77 |
| win | <5.0 | ✅learned | 283 | 0.757 |
| win | <10.0 | ✅learned | 129 | 0.462 |
| win | <20.0 | ✅learned | 34 | 0.237 |
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
_auto-generated by claude_snapshot.py at 2026-10-01T14:50:01.391004+09:00_