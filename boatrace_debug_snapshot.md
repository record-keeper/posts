# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-06T18:40:02.485808+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×40 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×29 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×64  [2026-07-06T18:08:17]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×64  [2026-07-06T18:08:17]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×32  [2026-07-06T18:08:17]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-07-06T18:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×16  [2026-07-06T17:54:47]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×54  [2026-07-06T17:34:23]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-07-06T17:30:06]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_BET_VOLUME_DROP  ×4  [2026-07-06T11:01:33]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-06T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S00: n=167<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-06T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=78<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-06T06:00:15]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=14 pred=0.2291 actual=0.0714 gap=+0.1577`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-07-06T06:00:15]
- key: `ORPHAN_SCAN|161 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-06T06:00:15]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1746 actual=0.4286 gap=-0.2540`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-06T06:00:15]
- key: `ROI_STAT|S00: n=167 hit%=28.7% hit_CI[Bonf]=[19.8,39.7]% ROI=0.78 ROI_boot95=[0.57,1.00]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-06T06:00:15]
- key: `ROI_STAT|S01_NAKAANA1: n=149 hit%=32.2% hit_CI[Bonf]=[22.4,44.0]% ROI=0.88 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-06T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=149<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-06T06:00:15]
- key: `ROI_STAT|S02_TETSUBAN: n=78 hit%=38.5% hit_CI[Bonf]=[24.4,54.7]% ROI=0.66 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-06T06:00:15]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=31.4% ROI=0.94 (コスト 10,200/回収 9,600)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-06T06:00:15]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=42 hit%=26.2% ROI=0.63 (コスト 9,900/回収 6,240)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-06T06:00:15]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=93 hit%=31.2% ROI=0.76 (コスト 21,600/回収 16,480)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 6.97MB / last modified 2026-07-06T18:39:06.750414+09:00

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
parsed
2026-07-06 18:37:29,394 [INFO] scraper: odds2t: 28/30 parsed
2026-07-06 18:37:29,396 [INFO] scraper: odds2f: 15/15 parsed
2026-07-06 18:37:30,511 [INFO] scraper: odds_win: 4/6 parsed
2026-07-06 18:37:30,511 [INFO] scraper: fetch_race 01/8: boats=6 odds=187/191
2026-07-06 18:37:30,521 [INFO] predictor: CALIBRATION_MODE=on
2026-07-06 18:37:30,522 [INFO] predictor: combos: {'win': 4, '2t': 28, '3t': 120}
2026-07-06 18:37:30,532 [INFO] run_cycle: fetched 01/8 [scan]: 152 combos
2026-07-06 18:37:30,671 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-06 18:38:06,192 [INFO] run_cycle: === run_cycle 18:38:06 ===
2026-07-06 18:38:06,192 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-06 18:38:06,193 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-06 18:38:06,283 [INFO] predictor: Models loaded OK
2026-07-06 18:38:18,797 [INFO] scraper: odds3t: 120/120 parsed
2026-07-06 18:38:19,937 [INFO] scraper: odds3f: 20/20 parsed
2026-07-06 18:38:21,073 [INFO] scraper: odds2t: 30/30 parsed
2026-07-06 18:38:21,074 [INFO] scraper: odds2f: 15/15 parsed
2026-07-06 18:38:22,315 [INFO] scraper: odds_win: 6/6 parsed
2026-07-06 18:38:22,315 [INFO] scraper: fetch_race 12/8: boats=6 odds=191/191
2026-07-06 18:38:22,326 [INFO] predictor: CALIBRATION_MODE=on
2026-07-06 18:38:22,327 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-06 18:38:22,334 [INFO] run_cycle: fetched 12/8 [final]: 156 combos
2026-07-06 18:38:22,554 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-06 18:39:05,930 [INFO] run_cycle: === run_cycle 18:39:05 ===
2026-07-06 18:39:05,930 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-06 18:39:05,930 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-06 18:39:06,003 [INFO] predictor: Models loaded OK
2026-07-06 18:39:06,150 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 62
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 62
  }
]
```

## Phase別通知記録 (24h)
{'final': 23, 'result': 14, 'scan': 25}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 155
  FINAL_MISSING: 40
  CIRCUIT_BREAKER_TRIP: 29
  CIRCUIT_BREAKER_NO_ACTION: 21
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 5
  ANOMALY_SCAN_FINAL_RATIO: 5
  ANOMALY_BET_VOLUME_DROP: 3
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 35 | 10 | 10,500 | 6,900 | -3,600 | 0.657 |
| S01_NAKAANA1 | 36 | 8 | 7,200 | 4,440 | -2,760 | 0.617 |
| S02_TETSUBAN | 25 | 13 | 5,000 | 4,980 | -20 | 0.996 |

## 直近アラート (24h・新しい順)
```
[18:36:06] FINAL_MISSING: {"deadline": "2026-07-06T13:03:00+09:00", "kind": "FINAL_MISSING", "nid": "2026070605041303", "sid": "S00"}
[18:28:06] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[18:28:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 841}
[18:26:32] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 837}
[18:25:46] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 838}
[18:24:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 857}
[18:23:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 853}
[18:22:07] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 868}
[18:21:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 869}
[18:20:10] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 864}
```

## 本日残レース: 23件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 109件 締切済
- 通知発射: scan=20 nid / final=18 nid / result=11 nid
- predictions: 14 / うち結果DB記録済: 12
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 6件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 017R | win | 1 | 0.5891 | 4.1 | 2.42 | 200 | scan=4.1 drift=+0.0% | 18:18:22 |
| S00 | 017R | win | 1 | 0.5891 | 4.1 | 2.42 | 300 | scan=4.1 drift=+0.0% | 18:18:21 |
| S02_TETSUBAN | 076R | win | 1 | 0.5891 | 2.1 | 1.24 | 200 | scan=2.1 drift=+0.0% | 18:01:20 |
| S01_NAKAANA1 | 124R | win | 1 | 0.5123 | 3.4 | 1.74 | 200 | scan=3.2 drift=+6.2% | 16:58:21 |
| S01_NAKAANA1 | 012R | win | 1 | 0.3177 | 3.0 | 0.95 | 200 | scan=- drift=- | 15:56:33 |
| S01_NAKAANA1 | 047R | win | 1 | 0.4989 | 4.3 | 2.15 | 200 | scan=4.2 drift=+2.4% | 14:57:24 |
| S00 | 047R | win | 1 | 0.4989 | 4.3 | 2.15 | 300 | scan=4.2 drift=+2.4% | 14:57:22 |
| S00 | 1811R | win | 1 | 0.0754 | 5.0 | 0.38 | 300 | scan=4.5 drift=+11.1% | 13:35:21 |
| S00 | 1810R | win | 1 | 0.3177 | 5.0 | 1.59 | 300 | scan=10.6 drift=-52.8% | 13:02:21 |
| S02_TETSUBAN | 2110R | win | 1 | 0.5891 | 2.1 | 1.24 | 200 | scan=2.4 drift=-12.5% | 12:46:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 54 | +12.2% | -60.8% | +584.6% | 15 | 4 | 29 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 452.4s |
| **Latency** (scan→final max) | 611.9s |
| **Traffic** (notifications 24h) | 62 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 1,200円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 397 | 0.4786 | 0.3199 | +0.1587 | 🟡+33% | 0.2381 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 166 | 0.4405 | 0.2892 | 0.2220 | 🔴-0.08 | 0.778 |
| S01_NAKAANA1 | win | 151 | 0.4876 | 0.3179 | 0.2430 | 🔴-0.12 | 0.866 |
| S02_TETSUBAN | win | 80 | 0.5407 | 0.3875 | 0.2620 | 🔴-0.10 | 0.671 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 7 | 0.1746 | 0.4286 | 🔴-0.2540 |
| 0.20-0.30 | 14 | 0.2291 | 0.0714 | 🔴+0.1577 |
| 0.30-0.50 | 137 | 0.4198 | 0.2920 | 🔴+0.1278 |
| 0.50+ | 235 | 0.5434 | 0.3532 | 🔴+0.1902 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 62 | 0.755 |
| win | <5.0 | ✅learned | 121 | 0.714 |
| win | <10.0 | ✅learned | 65 | 0.479 |
| win | <20.0 | ✅learned | 19 | 0.212 |
| win | <50.0 | ⚠️fallback | 2 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-07-06T18:40:02.485808+09:00_