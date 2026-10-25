# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-25T11:20:02.344081+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×54 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×54 (24h)
- 🟡 FINAL_MISSING×53 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×32  [2026-10-25T11:03:28]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×32  [2026-10-25T11:03:28]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×16  [2026-10-25T11:03:28]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×32  [2026-10-25T10:41:51]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-10-25T10:30:10]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-10-25T10:30:10]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×40  [2026-10-25T09:50:42]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-25T06:00:31]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=76<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-25T06:00:31]
- key: `INSUFFICIENT_SAMPLE|S00: n=186<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-25T06:00:31]
- key: `ORPHAN_SCAN|163 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-25T06:00:31]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=193<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-25T06:00:31]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1269 actual=0.3333 gap=-0.2064`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-25T06:00:31]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=66 hit%=31.8% ROI=0.83 (コスト 15,700/回収 13,040)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-25T06:00:31]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=8 pred=0.2288 actual=0.2500 gap=-0.0212`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-25T06:00:31]
- key: `DRIFT_BUCKET|drift ≤-30%: n=27 hit%=48.1% ROI=1.23 (コスト 7,800/回収 9,630)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-10-25T06:00:31]
- key: `ROI_STAT|S00: n=186 hit%=29.6% hit_CI[Bonf]=[21.0,39.9]% ROI=0.80 ROI_boot95=[0.59,1.02]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-25T06:00:31]
- key: `ROI_STAT|S01_NAKAANA1: n=193 hit%=33.2% hit_CI[Bonf]=[24.3,43.5]% ROI=0.91 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-25T06:00:31]
- key: `ROI_STAT|S02_TETSUBAN: n=76 hit%=51.3% hit_CI[Bonf]=[35.5,66.9]% ROI=0.93 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-25T06:00:31]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=47 hit%=34.0% ROI=0.75 (コスト 11,200/回収 8,450)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-25T06:00:31]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=89 hit%=40.4% ROI=1.12 (コスト 20,100/回収 22,540)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 16.78MB / last modified 2026-10-25T11:19:30.134886+09:00

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
rsed
2026-10-25 11:18:19,943 [INFO] scraper: fetch_race 04/2: boats=6 odds=191/191
2026-10-25 11:18:19,947 [INFO] predictor: CALIBRATION_MODE=on
2026-10-25 11:18:19,948 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-25 11:18:19,953 [INFO] run_cycle: fetched 04/2 [final]: 156 combos
2026-10-25 11:18:20,658 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-25 11:19:05,089 [INFO] run_cycle: === run_cycle 11:19:05 ===
2026-10-25 11:19:05,089 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-25 11:19:05,089 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-25 11:19:05,167 [INFO] predictor: Models loaded OK
2026-10-25 11:19:17,599 [INFO] scraper: odds3t: 120/120 parsed
2026-10-25 11:19:18,690 [INFO] scraper: odds3f: 20/20 parsed
2026-10-25 11:19:19,789 [INFO] scraper: odds2t: 30/30 parsed
2026-10-25 11:19:19,791 [INFO] scraper: odds2f: 15/15 parsed
2026-10-25 11:19:20,933 [INFO] scraper: odds_win: 5/6 parsed
2026-10-25 11:19:20,933 [INFO] scraper: fetch_race 14/7: boats=6 odds=190/191
2026-10-25 11:19:20,937 [INFO] predictor: CALIBRATION_MODE=on
2026-10-25 11:19:20,937 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-10-25 11:19:20,941 [INFO] run_cycle: fetched 14/7 [scan]: 155 combos
2026-10-25 11:19:24,489 [INFO] scraper: odds3t: 120/120 parsed
2026-10-25 11:19:25,587 [INFO] scraper: odds3f: 20/20 parsed
2026-10-25 11:19:26,724 [INFO] scraper: odds2t: 28/30 parsed
2026-10-25 11:19:26,780 [INFO] scraper: odds2f: 11/15 parsed
2026-10-25 11:19:27,899 [INFO] scraper: odds_win: 5/6 parsed
2026-10-25 11:19:27,899 [INFO] scraper: fetch_race 05/3: boats=6 odds=184/191
2026-10-25 11:19:27,901 [INFO] predictor: CALIBRATION_MODE=on
2026-10-25 11:19:27,901 [INFO] predictor: combos: {'win': 5, '2t': 28, '3t': 120}
2026-10-25 11:19:27,905 [INFO] run_cycle: fetched 05/3 [scan]: 153 combos
2026-10-25 11:19:28,188 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 73
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 73
  }
]
```

## Phase別通知記録 (24h)
{'final': 31, 'result': 18, 'scan': 24}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 213
  CIRCUIT_BREAKER_TRIP: 54
  FINAL_MISSING: 53
  CIRCUIT_BREAKER_NO_ACTION: 34
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 8
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 41 | 10 | 12,300 | 7,410 | -4,890 | 0.602 |
| S01_NAKAANA1 | 50 | 11 | 10,000 | 4,440 | -5,560 | 0.444 |
| S02_TETSUBAN | 11 | 5 | 2,200 | 2,340 | +140 | 1.064 |

## 直近アラート (24h・新しい順)
```
[11:17:34] CIRCUIT_BREAKER_TRIP: {"cost": 10000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 50, "payout": 4440, "roi_7d": 0.444, "sid": "S01_NAKAANA1"}
[11:17:34] CIRCUIT_BREAKER_TRIP: {"cost": 12300, "kind": "CIRCUIT_BREAKER_TRIP", "n": 41, "payout": 7410, "roi_7d": 0.602, "sid": "S00"}
[11:16:36] CIRCUIT_BREAKER_TRIP: {"cost": 10000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 50, "payout": 4120, "roi_7d": 0.412, "sid": "S01_NAKAANA1"}
[11:14:40] CIRCUIT_BREAKER_TRIP: {"cost": 10200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 51, "payout": 4860, "roi_7d": 0.476, "sid": "S01_NAKAANA1"}
[11:12:54] CIRCUIT_BREAKER_TRIP: {"cost": 10400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 52, "payout": 4860, "roi_7d": 0.467, "sid": "S01_NAKAANA1"}
[11:03:27] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:03:27] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[11:03:27] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[11:00:30] CIRCUIT_BREAKER_TRIP: {"cost": 12600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 42, "payout": 8520, "roi_7d": 0.676, "sid": "S00"}
[10:57:47] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.2, "baseline_mean": 0.8, "baseline_stdev": 0.056, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 6, "z_score": 3.58}
```

## 本日残レース: 133件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 35件 締切済
- 通知発射: scan=6 nid / final=7 nid / result=2 nid
- predictions: 3 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 041R | win | 1 | 0.4989 | 4.0 | 2.00 | 300 | scan=4.5 drift=-11.1% | 10:49:45 |
| S01_NAKAANA1 | 082R | win | 1 | 0.5686 | 3.7 | 2.10 | 200 | scan=- drift=- | 10:46:28 |
| S01_NAKAANA1 | 061R | win | 1 | 0.5719 | 3.3 | 1.89 | 200 | scan=- drift=- | 10:39:19 |
| S01_NAKAANA1 | 246R | win | 1 | 0.4111 | 3.4 | 1.40 | 200 | scan=3.8 drift=-10.5% | 17:47:19 |
| S00 | 243R | win | 1 | 0.5334 | 4.7 | 2.51 | 300 | scan=- drift=- | 16:18:31 |
| S01_NAKAANA1 | 121R | win | 1 | 0.5990 | 3.0 | 1.80 | 200 | scan=3.1 drift=-3.2% | 15:15:22 |
| S00 | 049R | win | 1 | 0.5735 | 7.9 | 4.53 | 300 | scan=8.2 drift=-3.7% | 14:38:19 |
| S01_NAKAANA1 | 098R | win | 1 | 0.5334 | 4.7 | 2.51 | 200 | scan=- drift=- | 13:53:24 |
| S00 | 098R | win | 1 | 0.5334 | 4.7 | 2.51 | 300 | scan=- drift=- | 13:53:19 |
| S01_NAKAANA1 | 1011R | win | 1 | 0.5123 | 3.3 | 1.69 | 200 | scan=- drift=- | 13:47:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 58 | +27.6% | -52.3% | +495.8% | 9 | 2 | 34 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 490.6s |
| **Latency** (scan→final max) | 618.7s |
| **Traffic** (notifications 24h) | 73 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 454 | 0.4801 | 0.3502 | +0.1298 | 🟡+27% | 0.2397 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 184 | 0.4406 | 0.2935 | 0.2324 | 🔴-0.12 | 0.803 |
| S01_NAKAANA1 | win | 194 | 0.4926 | 0.3402 | 0.2398 | 🔴-0.07 | 0.923 |
| S02_TETSUBAN | win | 76 | 0.5436 | 0.5132 | 0.2574 | 🔴-0.03 | 0.934 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 5 | 0.1226 | 0.2000 | 🔴-0.0774 |
| 0.15-0.20 | 8 | 0.1854 | 0.0000 | 🔴+0.1854 |
| 0.20-0.30 | 8 | 0.2288 | 0.2500 | ✅-0.0212 |
| 0.30-0.50 | 157 | 0.4117 | 0.3057 | 🔴+0.1059 |
| 0.50+ | 275 | 0.5429 | 0.3891 | 🔴+0.1539 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 192 | 0.781 |
| win | <5.0 | ✅learned | 349 | 0.744 |
| win | <10.0 | ✅learned | 153 | 0.454 |
| win | <20.0 | ✅learned | 43 | 0.254 |
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
_auto-generated by claude_snapshot.py at 2026-10-25T11:20:02.344081+09:00_