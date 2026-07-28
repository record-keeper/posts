# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-28T15:10:01.180822+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×25 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×25 (24h)
- 🟡 FINAL_MISSING×18 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×6  [2026-07-28T15:03:30]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×12  [2026-07-28T15:03:30]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×6  [2026-07-28T15:03:30]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-07-28T14:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-07-28T14:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×32  [2026-07-28T13:52:39]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×14  [2026-07-28T12:05:44]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-28T06:00:23]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=79<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-07-28T06:00:23]
- key: `ORPHAN_SCAN|173 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-28T06:00:23]
- key: `INSUFFICIENT_SAMPLE|S00: n=179<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-28T06:00:23]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=13 pred=0.2273 actual=0.3077 gap=-0.0804`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-28T06:00:23]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=165<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-28T06:00:23]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=7 pred=0.1262 actual=0.1429 gap=-0.0167`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-28T06:00:23]
- key: `DRIFT_BUCKET|drift ≥+30%: n=36 hit%=22.2% ROI=0.61 (コスト 10,000/回収 6,060)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-28T06:00:23]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=8 pred=0.1785 actual=0.3750 gap=-0.1965`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-28T06:00:23]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=135 pred=0.4387 actual=0.3037 gap=+0.1350`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-28T06:00:23]
- key: `ROI_STAT|S00: n=179 hit%=27.4% hit_CI[Bonf]=[18.9,37.8]% ROI=0.74 ROI_boot95=[0.53,0.97]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-28T06:00:23]
- key: `ROI_STAT|S01_NAKAANA1: n=165 hit%=27.3% hit_CI[Bonf]=[18.5,38.2]% ROI=0.74 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-28T06:00:23]
- key: `ROI_STAT|S02_TETSUBAN: n=79 hit%=50.6% hit_CI[Bonf]=[35.1,66.0]% ROI=0.99 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-28T06:00:23]
- key: `DRIFT_BUCKET|drift ≤-30%: n=32 hit%=31.2% ROI=0.65 (コスト 9,400/回収 6,090)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 8.88MB / last modified 2026-07-28T15:08:39.518802+09:00

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
ed out. (read timeout=10), retry in 1s
2026-07-28 15:09:25,831 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=8&jcd=16&hd=20260728: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-07-28 15:09:38,883 [WARNING] scraper: fetch error (3/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=8&jcd=16&hd=20260728: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-07-28 15:09:38,883 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/racelist?rno=8&jcd=16&hd=20260728
2026-07-28 15:09:38,883 [ERROR] scraper: racelist fetch failed: jcd=16 rno=8
2026-07-28 15:09:38,883 [WARNING] run_cycle: fetch None: 16/8
2026-07-28 15:09:50,243 [INFO] scraper: odds3t: 120/120 parsed
2026-07-28 15:09:51,330 [INFO] scraper: odds3f: 20/20 parsed
2026-07-28 15:09:52,457 [INFO] scraper: odds2t: 28/30 parsed
2026-07-28 15:09:52,459 [INFO] scraper: odds2f: 13/15 parsed
2026-07-28 15:09:53,582 [INFO] scraper: odds_win: 5/6 parsed
2026-07-28 15:09:53,582 [INFO] scraper: fetch_race 09/10: boats=6 odds=186/191
2026-07-28 15:09:53,585 [INFO] predictor: CALIBRATION_MODE=on
2026-07-28 15:09:53,585 [INFO] predictor: combos: {'win': 5, '2t': 28, '3t': 120}
2026-07-28 15:09:53,589 [INFO] run_cycle: fetched 09/10 [scan]: 153 combos
2026-07-28 15:09:56,995 [INFO] scraper: odds3t: 120/120 parsed
2026-07-28 15:09:58,076 [INFO] scraper: odds3f: 20/20 parsed
2026-07-28 15:09:59,190 [INFO] scraper: odds2t: 30/30 parsed
2026-07-28 15:09:59,191 [INFO] scraper: odds2f: 15/15 parsed
2026-07-28 15:10:00,385 [INFO] scraper: odds_win: 3/6 parsed
2026-07-28 15:10:00,385 [INFO] scraper: fetch_race 24/1: boats=6 odds=188/191
2026-07-28 15:10:00,387 [INFO] predictor: CALIBRATION_MODE=on
2026-07-28 15:10:00,388 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-07-28 15:10:00,391 [INFO] run_cycle: fetched 24/1 [scan]: 153 combos

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
    "c": 46
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 46
  }
]
```

## Phase別通知記録 (24h)
{'final': 18, 'result': 12, 'scan': 16}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 123
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 25
  FINAL_MISSING: 18
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 41 | 8 | 12,300 | 5,550 | -6,750 | 0.451 |
| S01_NAKAANA1 | 33 | 8 | 6,600 | 6,100 | -500 | 0.924 |
| S02_TETSUBAN | 18 | 10 | 3,600 | 3,380 | -220 | 0.939 |

## 直近アラート (24h・新しい順)
```
[15:03:29] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[15:03:29] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[15:03:29] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[14:37:04] CIRCUIT_BREAKER_TRIP: {"cost": 12300, "kind": "CIRCUIT_BREAKER_TRIP", "n": 41, "payout": 5550, "roi_7d": 0.451, "sid": "S00"}
[14:23:18] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 950}
[14:22:25] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 953}
[14:21:43] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 934}
[14:20:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 951}
[14:19:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 967}
[14:18:33] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 968}
```

## 本日残レース: 70件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 74件 締切済
- 通知発射: scan=11 nid / final=13 nid / result=9 nid
- predictions: 9 / うち結果DB記録済: 9
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 045R | win | 1 | 0.5334 | 4.5 | 2.40 | 200 | scan=- drift=- | 13:51:18 |
| S02_TETSUBAN | 117R | win | 1 | 0.5334 | 2.5 | 1.33 | 200 | scan=- drift=- | 13:46:19 |
| S00 | 165R | win | 1 | 0.5174 | 11.2 | 5.79 | 300 | scan=12.0 drift=-6.7% | 13:36:42 |
| S01_NAKAANA1 | 164R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=- drift=- | 13:05:30 |
| S01_NAKAANA1 | 043R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=3.5 drift=+0.0% | 12:50:31 |
| S02_TETSUBAN | 2110R | win | 1 | 0.4923 | 2.7 | 1.33 | 200 | scan=2.4 drift=+12.5% | 12:41:18 |
| S02_TETSUBAN | 034R | win | 1 | 0.4111 | 2.5 | 1.03 | 200 | scan=2.1 drift=+19.0% | 12:32:50 |
| S02_TETSUBAN | 161R | win | 1 | 0.5735 | 2.3 | 1.32 | 200 | scan=- drift=- | 11:46:43 |
| S01_NAKAANA1 | 216R | win | 1 | 0.5174 | 4.6 | 2.38 | 200 | scan=- drift=- | 10:42:30 |
| S01_NAKAANA1 | 124R | win | 1 | 0.5095 | 3.0 | 1.53 | 200 | scan=- drift=- | 17:04:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 43 | +9.1% | -86.1% | +198.5% | 13 | 8 | 30 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 443.8s |
| **Latency** (scan→final max) | 624.8s |
| **Traffic** (notifications 24h) | 46 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |
| **Saturation** (S02_TETSUBAN) | 800円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 421 | 0.4638 | 0.3112 | +0.1527 | 🟡+33% | 0.2327 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 178 | 0.4202 | 0.2640 | 0.2237 | 🔴-0.15 | 0.706 |
| S01_NAKAANA1 | win | 161 | 0.4755 | 0.2671 | 0.2354 | 🔴-0.20 | 0.765 |
| S02_TETSUBAN | win | 82 | 0.5357 | 0.5000 | 0.2468 | ✅+0.01 | 0.973 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 7 | 0.1262 | 0.1429 | ✅-0.0167 |
| 0.15-0.20 | 8 | 0.1785 | 0.3750 | 🔴-0.1965 |
| 0.20-0.30 | 13 | 0.2273 | 0.3077 | 🔴-0.0804 |
| 0.30-0.50 | 166 | 0.4163 | 0.2530 | 🔴+0.1633 |
| 0.50+ | 223 | 0.5406 | 0.3632 | 🔴+0.1773 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 88 | 0.802 |
| win | <5.0 | ✅learned | 157 | 0.726 |
| win | <10.0 | ✅learned | 82 | 0.455 |
| win | <20.0 | ✅learned | 26 | 0.216 |
| win | <50.0 | ⚠️fallback | 6 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-07-28T15:10:01.180822+09:00_