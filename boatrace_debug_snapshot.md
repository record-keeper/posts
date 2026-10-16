# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-16T17:50:01.253345+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×28 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×3 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×10  [2026-10-16T17:31:29]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-10-16T17:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-10-16T17:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×86  [2026-10-16T17:07:38]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×43  [2026-10-16T17:07:38]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×49  [2026-10-16T17:01:10]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×4  [2026-10-16T11:23:59]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×20  [2026-10-16T11:13:25]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🟡 ORPHAN_SCAN  ×1  [2026-10-16T06:00:19]
- key: `ORPHAN_SCAN|156 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-16T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=87<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-16T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=170<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-16T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S00: n=180<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-10-16T06:00:19]
- key: `ROI_STAT|S00: n=180 hit%=26.7% hit_CI[Bonf]=[18.3,37.1]% ROI=0.73 ROI_boot95=[0.53,0.96]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-16T06:00:19]
- key: `ROI_STAT|S01_NAKAANA1: n=170 hit%=35.3% hit_CI[Bonf]=[25.6,46.3]% ROI=1.01 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-16T06:00:19]
- key: `ROI_STAT|S02_TETSUBAN: n=87 hit%=51.7% hit_CI[Bonf]=[36.8,66.3]% ROI=0.93 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-16T06:00:19]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=39.4% ROI=1.00 (コスト 9,500/回収 9,510)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-16T06:00:19]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=50 hit%=32.0% ROI=0.74 (コスト 11,800/回収 8,720)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-16T06:00:19]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=91 hit%=38.5% ROI=1.09 (コスト 21,000/回収 22,860)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-16T06:00:19]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=58 hit%=36.2% ROI=0.86 (コスト 13,800/回収 11,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-16T06:00:19]
- key: `DRIFT_BUCKET|drift ≥+30%: n=46 hit%=23.9% ROI=0.79 (コスト 11,800/回収 9,360)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 15.96MB / last modified 2026-10-16T17:49:45.465632+09:00

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
: 30/30 parsed
2026-10-16 17:48:19,374 [INFO] scraper: odds2f: 14/15 parsed
2026-10-16 17:48:20,466 [INFO] scraper: odds_win: 3/6 parsed
2026-10-16 17:48:20,466 [INFO] scraper: fetch_race 24/7: boats=6 odds=187/191
2026-10-16 17:48:20,469 [INFO] predictor: CALIBRATION_MODE=on
2026-10-16 17:48:20,469 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-10-16 17:48:20,473 [INFO] run_cycle: fetched 24/7 [scan]: 153 combos
2026-10-16 17:48:20,597 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-16 17:49:04,744 [INFO] run_cycle: === run_cycle 17:49:04 ===
2026-10-16 17:49:04,744 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-16 17:49:04,744 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-16 17:49:04,809 [INFO] predictor: Models loaded OK
2026-10-16 17:49:15,964 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=7&jcd=20&hd=20261016: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-16 17:49:27,000 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=7&jcd=20&hd=20261016: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-10-16 17:49:41,645 [INFO] scraper: odds3t: 120/120 parsed
2026-10-16 17:49:42,748 [INFO] scraper: odds3f: 20/20 parsed
2026-10-16 17:49:43,838 [INFO] scraper: odds2t: 30/30 parsed
2026-10-16 17:49:43,839 [INFO] scraper: odds2f: 14/15 parsed
2026-10-16 17:49:44,965 [INFO] scraper: odds_win: 4/6 parsed
2026-10-16 17:49:44,965 [INFO] scraper: fetch_race 20/7: boats=6 odds=188/191
2026-10-16 17:49:44,969 [INFO] predictor: CALIBRATION_MODE=on
2026-10-16 17:49:44,969 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-10-16 17:49:44,973 [INFO] run_cycle: fetched 20/7 [scan]: 154 combos
2026-10-16 17:49:45,111 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 28, 'result': 21, 'scan': 22}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 236
  FINAL_MISSING: 28
  CIRCUIT_BREAKER_NO_ACTION: 23
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 8
  CIRCUIT_BREAKER_TRIP: 3
  ANOMALY_SCAN_FINAL_RATIO: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 53 | 15 | 15,900 | 14,130 | -1,770 | 0.889 |
| S01_NAKAANA1 | 42 | 16 | 8,400 | 7,160 | -1,240 | 0.852 |
| S02_TETSUBAN | 23 | 14 | 4,600 | 5,000 | +400 | 1.087 |

## 直近アラート (24h・新しい順)
```
[17:47:04] FINAL_MISSING: {"deadline": "2026-10-16T17:17:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101601051717", "sid": "S00"}
[17:41:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 644}
[17:40:08] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 646}
[17:39:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 645}
[17:38:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 654}
[17:37:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 637}
[17:35:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 647}
[17:34:40] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 638}
[17:32:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 666}
[17:30:11] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 648}
```

## 本日残レース: 29件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 127件 締切済
- 通知発射: scan=16 nid / final=21 nid / result=18 nid
- predictions: 20 / うち結果DB記録済: 20
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 5件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 202R | win | 1 | 0.5735 | 2.7 | 1.55 | 200 | scan=- drift=- | 15:47:20 |
| S02_TETSUBAN | 0310R | win | 1 | 0.5735 | 2.0 | 1.15 | 200 | scan=- drift=- | 15:19:29 |
| S01_NAKAANA1 | 038R | win | 1 | 0.5031 | 4.0 | 2.01 | 200 | scan=- drift=- | 14:21:19 |
| S00 | 098R | win | 1 | 0.1957 | 5.0 | 0.98 | 300 | scan=- drift=- | 13:58:20 |
| S01_NAKAANA1 | 037R | win | 1 | 0.4989 | 4.7 | 2.34 | 200 | scan=4.7 drift=+0.0% | 13:53:20 |
| S01_NAKAANA1 | 026R | win | 1 | 0.5073 | 4.5 | 2.28 | 200 | scan=3.3 drift=+36.4% | 13:11:22 |
| S00 | 026R | win | 1 | 0.5073 | 4.5 | 2.28 | 300 | scan=7.1 drift=-36.6% | 13:11:20 |
| S00 | 035R | win | 1 | 0.4922 | 5.2 | 2.56 | 300 | scan=4.5 drift=+15.6% | 12:59:26 |
| S00 | 096R | win | 1 | 0.4989 | 8.8 | 4.39 | 300 | scan=6.0 drift=+46.7% | 12:53:20 |
| S00 | 109R | win | 1 | 0.5891 | 9.7 | 5.71 | 300 | scan=5.6 drift=+73.2% | 12:38:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 71 | +20.5% | -52.2% | +326.7% | 14 | 7 | 50 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 435.1s |
| **Latency** (scan→final max) | 602.0s |
| **Traffic** (notifications 24h) | 71 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 3,600円 used |
| **Saturation** (S01_NAKAANA1) | 1,200円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 436 | 0.4778 | 0.3601 | +0.1177 | 🟡+25% | 0.2445 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 180 | 0.4409 | 0.2778 | 0.2381 | 🔴-0.19 | 0.747 |
| S01_NAKAANA1 | win | 170 | 0.4908 | 0.3588 | 0.2444 | 🔴-0.06 | 1.032 |
| S02_TETSUBAN | win | 86 | 0.5292 | 0.5349 | 0.2579 | 🔴-0.04 | 0.955 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1269 | 0.3333 | 🔴-0.2064 |
| 0.15-0.20 | 6 | 0.1845 | 0.0000 | 🔴+0.1845 |
| 0.20-0.30 | 6 | 0.2287 | 0.3333 | 🔴-0.1046 |
| 0.30-0.50 | 159 | 0.4168 | 0.3208 | 🔴+0.0960 |
| 0.50+ | 255 | 0.5434 | 0.3961 | 🔴+0.1474 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 185 | 0.772 |
| win | <5.0 | ✅learned | 331 | 0.751 |
| win | <10.0 | ✅learned | 146 | 0.462 |
| win | <20.0 | ✅learned | 42 | 0.244 |
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
_auto-generated by claude_snapshot.py at 2026-10-16T17:50:01.253345+09:00_