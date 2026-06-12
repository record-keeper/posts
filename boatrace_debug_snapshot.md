# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-12T14:40:02.080243+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×46 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×68 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×46 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×3  [2026-06-12T14:37:06]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×37  [2026-06-12T14:03:40]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×111  [2026-06-12T14:03:40]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×37  [2026-06-12T14:03:40]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-12T14:00:08]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-12T14:00:08]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-12T14:00:08]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×31  [2026-06-12T13:58:46]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-12T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1254 actual=0.1667 gap=-0.0412`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-12T06:00:13]
- key: `ROI_STAT|S00: n=150 hit%=28.7% hit_CI[Bonf]=[19.4,40.2]% ROI=0.85 ROI_boot95=[0.59,1.14]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-12T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S00: n=150<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-12T06:00:13]
- key: `ROI_STAT|S01_NAKAANA1: n=134 hit%=26.9% hit_CI[Bonf]=[17.4,39.0]% ROI=0.70 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-12T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=134<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-12T06:00:13]
- key: `ROI_STAT|S02_TETSUBAN: n=82 hit%=34.1% hit_CI[Bonf]=[21.1,50.1]% ROI=0.57 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-12T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=82<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-06-12T06:00:13]
- key: `ORPHAN_SCAN|143 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-12T06:00:13]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=34.3% ROI=1.00 (コスト 10,300/回収 10,290)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-12T06:00:13]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=35 hit%=17.1% ROI=0.35 (コスト 7,700/回収 2,710)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-12T06:00:13]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=70 hit%=28.6% ROI=0.57 (コスト 16,500/回収 9,420)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-12T06:00:13]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=35 hit%=20.0% ROI=0.72 (コスト 7,900/回収 5,660)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 4.92MB / last modified 2026-06-12T14:39:38.647154+09:00

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
2 14:38:28,616 [INFO] run_cycle: fetched 13/9 [scan]: 156 combos
2026-06-12 14:38:28,727 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-12 14:39:05,554 [INFO] run_cycle: === run_cycle 14:39:05 ===
2026-06-12 14:39:05,556 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-12 14:39:05,556 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-12 14:39:05,602 [INFO] predictor: Models loaded OK
2026-06-12 14:39:16,680 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=9&jcd=09&hd=20260612: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-06-12 14:39:28,312 [INFO] scraper: odds3t: 120/120 parsed
2026-06-12 14:39:29,389 [INFO] scraper: odds3f: 20/20 parsed
2026-06-12 14:39:30,506 [INFO] scraper: odds2t: 30/30 parsed
2026-06-12 14:39:30,507 [INFO] scraper: odds2f: 15/15 parsed
2026-06-12 14:39:31,585 [INFO] scraper: odds_win: 6/6 parsed
2026-06-12 14:39:31,585 [INFO] scraper: fetch_race 09/9: boats=6 odds=191/191
2026-06-12 14:39:31,598 [INFO] predictor: CALIBRATION_MODE=on
2026-06-12 14:39:31,598 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-12 14:39:31,605 [INFO] run_cycle: fetched 09/9 [final]: 156 combos
2026-06-12 14:39:35,177 [INFO] scraper: odds3t: 120/120 parsed
2026-06-12 14:39:36,286 [INFO] scraper: odds3f: 20/20 parsed
2026-06-12 14:39:37,372 [INFO] scraper: odds2t: 30/30 parsed
2026-06-12 14:39:37,373 [INFO] scraper: odds2f: 15/15 parsed
2026-06-12 14:39:38,447 [INFO] scraper: odds_win: 4/6 parsed
2026-06-12 14:39:38,447 [INFO] scraper: fetch_race 03/9: boats=6 odds=189/191
2026-06-12 14:39:38,457 [INFO] predictor: CALIBRATION_MODE=on
2026-06-12 14:39:38,457 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-06-12 14:39:38,465 [INFO] run_cycle: fetched 03/9 [scan]: 154 combos
2026-06-12 14:39:38,580 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 71
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 71
  }
]
```

## Phase別通知記録 (24h)
{'final': 27, 'result': 16, 'scan': 28}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 123
  FINAL_MISSING: 68
  CIRCUIT_BREAKER_NO_ACTION: 51
  CIRCUIT_BREAKER_TRIP: 46
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 9
  ANOMALY_BET_VOLUME_SPIKE: 4
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 40 | 13 | 12,000 | 11,880 | -120 | 0.99 |
| S01_NAKAANA1 | 34 | 11 | 6,800 | 5,780 | -1,020 | 0.85 |
| S02_TETSUBAN | 28 | 7 | 5,600 | 2,040 | -3,560 | 0.364 |

## 直近アラート (24h・新しい順)
```
[14:37:06] FINAL_MISSING: {"deadline": "2026-06-12T10:04:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061214041004", "sid": "S00"}
[14:28:32] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 991}
[14:27:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 982}
[14:26:31] FINAL_MISSING: {"deadline": "2026-06-12T13:56:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061203071356", "sid": "S00"}
[14:26:31] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1000}
[14:24:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1014}
[14:23:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1019}
[14:22:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1010}
[14:21:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1001}
[14:20:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1011}
```

## 本日残レース: 62件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 82件 締切済
- 通知発射: scan=11 nid / final=16 nid / result=11 nid
- predictions: 11 / うち結果DB記録済: 11
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 5件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 097R | win | 1 | 0.5891 | 2.5 | 1.47 | 200 | scan=2.3 drift=+8.7% | 13:38:38 |
| S01_NAKAANA1 | 165R | win | 1 | 0.3177 | 4.1 | 1.30 | 200 | scan=- drift=- | 12:47:21 |
| S00 | 164R | win | 1 | 0.5719 | 14.2 | 8.12 | 300 | scan=- drift=- | 12:17:33 |
| S01_NAKAANA1 | 238R | win | 1 | 0.5123 | 3.6 | 1.84 | 200 | scan=- drift=- | 11:49:33 |
| S01_NAKAANA1 | 032R | win | 1 | 0.3177 | 3.1 | 0.98 | 200 | scan=- drift=- | 11:39:22 |
| S01_NAKAANA1 | 147R | win | 1 | 0.5334 | 3.3 | 1.76 | 200 | scan=- drift=- | 11:31:21 |
| S00 | 113R | win | 1 | 0.2290 | 4.5 | 1.03 | 300 | scan=- drift=- | 11:21:44 |
| S00 | 107R | win | 1 | 0.5123 | 6.0 | 3.07 | 300 | scan=5.2 drift=+15.4% | 11:09:22 |
| S02_TETSUBAN | 132R | win | 1 | 0.5334 | 2.5 | 1.33 | 200 | scan=- drift=- | 10:59:20 |
| S01_NAKAANA1 | 144R | win | 1 | 0.3177 | 3.3 | 1.05 | 200 | scan=3.1 drift=+6.5% | 10:01:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 57 | +6.3% | -82.9% | +274.6% | 18 | 8 | 31 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 492.2s |
| **Latency** (scan→final max) | 609.8s |
| **Traffic** (notifications 24h) | 71 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 1,200円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 366 | 0.4698 | 0.2951 | +0.1747 | 🟡+37% | 0.2392 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 147 | 0.4197 | 0.2857 | 0.2179 | 🔴-0.07 | 0.875 |
| S01_NAKAANA1 | win | 136 | 0.4862 | 0.2721 | 0.2476 | 🔴-0.25 | 0.744 |
| S02_TETSUBAN | win | 83 | 0.5316 | 0.3494 | 0.2629 | 🔴-0.16 | 0.572 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 5 | 0.1231 | 0.2000 | 🔴-0.0769 |
| 0.15-0.20 | 5 | 0.1835 | 0.2000 | ✅-0.0165 |
| 0.20-0.30 | 7 | 0.2244 | 0.2857 | 🔴-0.0613 |
| 0.30-0.50 | 132 | 0.4180 | 0.2348 | 🔴+0.1832 |
| 0.50+ | 209 | 0.5416 | 0.3493 | 🔴+0.1924 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 38 | 0.724 |
| win | <5.0 | ✅learned | 72 | 0.727 |
| win | <10.0 | ✅learned | 47 | 0.513 |
| win | <20.0 | ✅learned | 14 | 0.21 |
| win | <50.0 | ⚠️fallback | 1 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-06-12T14:40:02.080243+09:00_