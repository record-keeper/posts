# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-30T14:20:01.739380+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×25 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×55 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×25 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×34  [2026-07-30T14:03:34]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×34  [2026-07-30T14:03:34]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×17  [2026-07-30T14:03:34]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×20  [2026-07-30T14:00:28]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-07-30T14:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-07-30T14:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×33  [2026-07-30T12:07:46]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×31  [2026-07-30T10:46:39]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-30T06:00:06]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=82<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-07-30T06:00:06]
- key: `ORPHAN_SCAN|173 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-30T06:00:06]
- key: `INSUFFICIENT_SAMPLE|S00: n=179<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-30T06:00:06]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=8 pred=0.1785 actual=0.3750 gap=-0.1965`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-30T06:00:06]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=12 pred=0.2272 actual=0.2500 gap=-0.0228`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-30T06:00:06]
- key: `ROI_STAT|S00: n=179 hit%=26.8% hit_CI[Bonf]=[18.4,37.2]% ROI=0.69 ROI_boot95=[0.49,0.91]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-30T06:00:06]
- key: `ROI_STAT|S01_NAKAANA1: n=158 hit%=25.3% hit_CI[Bonf]=[16.7,36.4]% ROI=0.72 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-30T06:00:06]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=158<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-30T06:00:06]
- key: `ROI_STAT|S02_TETSUBAN: n=82 hit%=51.2% hit_CI[Bonf]=[35.9,66.3]% ROI=1.00 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-30T06:00:06]
- key: `DRIFT_BUCKET|drift ≤-30%: n=28 hit%=28.6% ROI=0.46 (コスト 8,200/回収 3,780)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-30T06:00:06]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=39 hit%=35.9% ROI=0.87 (コスト 9,600/回収 8,380)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-30T06:00:06]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=74 hit%=31.1% ROI=0.72 (コスト 17,200/回収 12,470)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 9.02MB / last modified 2026-07-30T14:19:43.589860+09:00

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
 30/30 parsed
2026-07-30 14:18:24,324 [INFO] scraper: odds2f: 15/15 parsed
2026-07-30 14:18:25,397 [INFO] scraper: odds_win: 6/6 parsed
2026-07-30 14:18:25,397 [INFO] scraper: fetch_race 04/6: boats=6 odds=191/191
2026-07-30 14:18:25,399 [INFO] predictor: CALIBRATION_MODE=on
2026-07-30 14:18:25,399 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-30 14:18:25,403 [INFO] run_cycle: fetched 04/6 [scan]: 156 combos
2026-07-30 14:18:25,509 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-30 14:19:03,502 [INFO] run_cycle: === run_cycle 14:19:03 ===
2026-07-30 14:19:03,502 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-30 14:19:03,502 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-30 14:19:03,530 [INFO] predictor: Models loaded OK
2026-07-30 14:19:14,563 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=5&jcd=22&hd=20260730: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-07-30 14:19:25,595 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=5&jcd=22&hd=20260730: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-07-30 14:19:39,983 [INFO] scraper: odds3t: 120/120 parsed
2026-07-30 14:19:41,104 [INFO] scraper: odds3f: 20/20 parsed
2026-07-30 14:19:42,186 [INFO] scraper: odds2t: 29/30 parsed
2026-07-30 14:19:42,187 [INFO] scraper: odds2f: 14/15 parsed
2026-07-30 14:19:43,268 [INFO] scraper: odds_win: 5/6 parsed
2026-07-30 14:19:43,269 [INFO] scraper: fetch_race 22/5: boats=6 odds=188/191
2026-07-30 14:19:43,273 [INFO] predictor: CALIBRATION_MODE=on
2026-07-30 14:19:43,273 [INFO] predictor: combos: {'win': 5, '2t': 29, '3t': 120}
2026-07-30 14:19:43,278 [INFO] run_cycle: fetched 22/5 [final]: 154 combos
2026-07-30 14:19:43,478 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 52
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 52
  }
]
```

## Phase別通知記録 (24h)
{'final': 20, 'result': 12, 'scan': 20}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 150
  FINAL_MISSING: 55
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 25
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 3
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 43 | 9 | 12,900 | 5,910 | -6,990 | 0.458 |
| S01_NAKAANA1 | 34 | 9 | 6,800 | 4,360 | -2,440 | 0.641 |
| S02_TETSUBAN | 17 | 9 | 3,400 | 2,960 | -440 | 0.871 |

## 直近アラート (24h・新しい順)
```
[14:03:34] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[14:03:34] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[14:03:34] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[14:02:03] CIRCUIT_BREAKER_TRIP: {"cost": 6800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 34, "payout": 4360, "roi_7d": 0.641, "sid": "S01_NAKAANA1"}
[14:00:27] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 8.7, "baseline_n_days": 7, "baseline_stdev": 2.8, "hour": 14, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 3, "z_score": -2.08}
[13:55:25] CIRCUIT_BREAKER_TRIP: {"cost": 12900, "kind": "CIRCUIT_BREAKER_TRIP", "n": 43, "payout": 5910, "roi_7d": 0.458, "sid": "S00"}
[13:33:33] FINAL_MISSING: {"deadline": "2026-07-30T13:03:00+09:00", "kind": "FINAL_MISSING", "nid": "2026073016031303", "sid": "S00"}
[13:32:28] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": 29.7, "final": 4.8, "kind": "LARGE_ODDS_DRIFT", "race": "164R", "scan": 3.7, "sid": "S01_NAKAANA1"}
[13:02:19] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:02:19] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
```

## 本日残レース: 66件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 66件 締切済
- 通知発射: scan=8 nid / final=8 nid / result=3 nid
- predictions: 3 / うち結果DB記録済: 3
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 164R | win | 1 | 0.5123 | 4.8 | 2.46 | 200 | scan=3.7 drift=+29.7% | 13:32:18 |
| S00 | 109R | win | 1 | 0.5123 | 9.5 | 4.87 | 300 | scan=5.2 drift=+82.7% | 12:11:19 |
| S01_NAKAANA1 | 187R | win | 1 | 0.4111 | 3.2 | 1.32 | 200 | scan=- drift=- | 11:28:30 |
| S00 | 196R | win | 1 | 0.5174 | 4.3 | 2.22 | 300 | scan=5.2 drift=-17.3% | 18:05:18 |
| S02_TETSUBAN | 1612R | win | 1 | 0.5735 | 2.2 | 1.26 | 200 | scan=- drift=- | 17:38:19 |
| S01_NAKAANA1 | 193R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=- drift=- | 16:44:20 |
| S02_TETSUBAN | 203R | win | 1 | 0.4989 | 2.6 | 1.30 | 200 | scan=2.7 drift=-3.7% | 16:35:19 |
| S00 | 229R | win | 1 | 0.5334 | 6.7 | 3.57 | 300 | scan=12.0 drift=-44.2% | 16:30:44 |
| S01_NAKAANA1 | 242R | win | 1 | 0.4989 | 4.0 | 2.00 | 200 | scan=- drift=- | 15:53:43 |
| S00 | 242R | win | 1 | 0.4989 | 8.4 | 4.19 | 300 | scan=8.0 drift=+5.0% | 15:52:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 49 | +17.7% | -86.1% | +375.6% | 13 | 8 | 34 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 457.7s |
| **Latency** (scan→final max) | 600.9s |
| **Traffic** (notifications 24h) | 52 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 415 | 0.4619 | 0.3084 | +0.1534 | 🟡+33% | 0.2328 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 175 | 0.4207 | 0.2686 | 0.2234 | 🔴-0.14 | 0.695 |
| S01_NAKAANA1 | win | 158 | 0.4715 | 0.2468 | 0.2346 | 🔴-0.26 | 0.701 |
| S02_TETSUBAN | win | 82 | 0.5313 | 0.5122 | 0.2492 | 🔴+0.00 | 1.004 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 8 | 0.1275 | 0.1250 | ✅+0.0025 |
| 0.15-0.20 | 8 | 0.1785 | 0.3750 | 🔴-0.1965 |
| 0.20-0.30 | 12 | 0.2272 | 0.2500 | ✅-0.0228 |
| 0.30-0.50 | 168 | 0.4168 | 0.2560 | 🔴+0.1609 |
| 0.50+ | 215 | 0.5402 | 0.3628 | 🔴+0.1774 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 91 | 0.796 |
| win | <5.0 | ✅learned | 161 | 0.717 |
| win | <10.0 | ✅learned | 84 | 0.45 |
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
_auto-generated by claude_snapshot.py at 2026-07-30T14:20:01.739380+09:00_