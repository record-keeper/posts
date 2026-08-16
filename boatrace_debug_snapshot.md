# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-16T12:40:01.386501+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×123 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×63 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×8 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-16T12:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-16T12:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-16T12:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×74  [2026-08-16T12:02:38]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×111  [2026-08-16T12:02:38]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×37  [2026-08-16T12:02:38]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×36  [2026-08-16T11:54:32]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-16T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=72<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-16T06:00:11]
- key: `ORPHAN_SCAN|205 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-16T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=175<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-16T06:00:11]
- key: `DRIFT_BUCKET|drift ≤-30%: n=38 hit%=21.1% ROI=0.62 (コスト 10,900/回収 6,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-16T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=9 pred=0.1189 actual=0.1111 gap=+0.0078`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-16T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=12 pred=0.1827 actual=0.0833 gap=+0.0994`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-16T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2228 actual=0.4444 gap=-0.2216`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-16T06:00:11]
- key: `ROI_STAT|S00: n=175 hit%=22.3% hit_CI[Bonf]=[14.6,32.5]% ROI=0.62 ROI_boot95=[0.42,0.85]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-16T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=173 hit%=20.2% hit_CI[Bonf]=[12.9,30.3]% ROI=0.66 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-16T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=173<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-16T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=72 hit%=50.0% hit_CI[Bonf]=[33.9,66.1]% ROI=0.81 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-16T06:00:11]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=37 hit%=35.1% ROI=1.04 (コスト 8,900/回収 9,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-16T06:00:11]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=77 hit%=24.7% ROI=0.57 (コスト 18,000/回収 10,330)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 10.65MB / last modified 2026-08-16T12:39:19.609026+09:00

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
3t: 120/120 parsed
2026-08-16 12:38:16,924 [INFO] scraper: odds3f: 20/20 parsed
2026-08-16 12:38:18,029 [INFO] scraper: odds2t: 30/30 parsed
2026-08-16 12:38:18,030 [INFO] scraper: odds2f: 14/15 parsed
2026-08-16 12:38:19,100 [INFO] scraper: odds_win: 6/6 parsed
2026-08-16 12:38:19,100 [INFO] scraper: fetch_race 11/5: boats=6 odds=190/191
2026-08-16 12:38:19,104 [INFO] predictor: CALIBRATION_MODE=on
2026-08-16 12:38:19,104 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-16 12:38:19,109 [INFO] run_cycle: fetched 11/5 [final]: 156 combos
2026-08-16 12:38:19,528 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-16 12:39:04,345 [INFO] run_cycle: === run_cycle 12:39:04 ===
2026-08-16 12:39:04,345 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-16 12:39:04,345 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-16 12:39:04,394 [INFO] predictor: Models loaded OK
2026-08-16 12:39:15,839 [INFO] scraper: odds3t: 120/120 parsed
2026-08-16 12:39:16,937 [INFO] scraper: odds3f: 20/20 parsed
2026-08-16 12:39:18,010 [INFO] scraper: odds2t: 30/30 parsed
2026-08-16 12:39:18,011 [INFO] scraper: odds2f: 14/15 parsed
2026-08-16 12:39:19,077 [INFO] scraper: odds_win: 6/6 parsed
2026-08-16 12:39:19,077 [INFO] scraper: fetch_race 18/9: boats=6 odds=190/191
2026-08-16 12:39:19,081 [INFO] predictor: CALIBRATION_MODE=on
2026-08-16 12:39:19,081 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-16 12:39:19,085 [INFO] run_cycle: fetched 18/9 [final]: 156 combos
2026-08-16 12:39:19,452 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-16 12:40:04,684 [INFO] run_cycle: === run_cycle 12:40:04 ===
2026-08-16 12:40:04,684 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-16 12:40:04,684 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-16 12:40:04,757 [INFO] predictor: Models loaded OK

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
    "c": 87
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 87
  }
]
```

## Phase別通知記録 (24h)
{'final': 29, 'result': 19, 'scan': 39}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 123
  CIRCUIT_BREAKER_TRIP: 63
  CIRCUIT_BREAKER_NO_ACTION: 51
  ANOMALY_SCRAPER_FAILURE_BURST: 23
  STRATEGY_CI_FAIL: 17
  CALIBRATION_DRIFT: 8
  ANOMALY_SCAN_FINAL_RATIO: 6
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 46 | 12 | 13,800 | 9,870 | -3,930 | 0.715 |
| S01_NAKAANA1 | 49 | 8 | 9,800 | 5,800 | -4,000 | 0.592 |
| S02_TETSUBAN | 20 | 9 | 4,000 | 2,480 | -1,520 | 0.62 |

## 直近アラート (24h・新しい順)
```
[12:31:10] CIRCUIT_BREAKER_TRIP: {"cost": 4000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 20, "payout": 2480, "roi_7d": 0.62, "sid": "S02_TETSUBAN"}
[12:24:38] CIRCUIT_BREAKER_TRIP: {"cost": 4200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 21, "payout": 2480, "roi_7d": 0.59, "sid": "S02_TETSUBAN"}
[12:20:27] FINAL_MISSING: {"deadline": "2026-08-16T11:50:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081610081150", "sid": "S00"}
[12:20:27] FINAL_MISSING: {"deadline": "2026-08-16T10:50:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081610061050", "sid": "S00"}
[12:13:20] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.24, "baseline_mean": 0.74, "baseline_stdev": 0.099, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 8, "z_score": -2.44}
[12:02:38] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:02:38] CIRCUIT_BREAKER_TRIP: {"cost": 4400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 22, "payout": 2800, "roi_7d": 0.636, "sid": "S02_TETSUBAN"}
[12:02:38] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[12:02:38] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[12:02:38] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
```

## 本日残レース: 138件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 192件 登録 / 54件 締切済
- 通知発射: scan=8 nid / final=4 nid / result=3 nid
- predictions: 3 / うち結果DB記録済: 3
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 5件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 174R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=4.1 drift=-26.8% | 12:04:20 |
| S01_NAKAANA1 | 147R | win | 1 | 0.5334 | 4.9 | 2.61 | 200 | scan=3.7 drift=+32.4% | 11:24:18 |
| S00 | 146R | win | 1 | 0.4111 | 6.2 | 2.55 | 300 | scan=13.8 drift=-55.1% | 10:52:19 |
| S01_NAKAANA1 | 248R | win | 1 | 0.4111 | 3.2 | 1.32 | 200 | scan=- drift=- | 18:44:18 |
| S00 | 128R | win | 1 | 0.5334 | 8.0 | 4.27 | 300 | scan=- drift=- | 18:25:19 |
| S01_NAKAANA1 | 014R | win | 1 | 0.5123 | 4.3 | 2.20 | 200 | scan=4.7 drift=-8.5% | 16:31:18 |
| S01_NAKAANA1 | 013R | win | 1 | 0.5334 | 3.8 | 2.03 | 200 | scan=3.0 drift=+26.7% | 16:05:18 |
| S02_TETSUBAN | 072R | win | 1 | 0.5123 | 2.0 | 1.02 | 200 | scan=- drift=- | 15:48:18 |
| S00 | 012R | win | 1 | 0.5891 | 4.1 | 2.42 | 300 | scan=- drift=- | 15:39:44 |
| S01_NAKAANA1 | 046R | win | 1 | 0.5334 | 4.3 | 2.29 | 200 | scan=4.2 drift=+2.4% | 14:23:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 70 | +8.6% | -62.9% | +287.7% | 19 | 8 | 38 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 494.0s |
| **Latency** (scan→final max) | 651.1s |
| **Traffic** (notifications 24h) | 87 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 416 | 0.4674 | 0.2644 | +0.2030 | 🟡+43% | 0.2368 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 173 | 0.4192 | 0.2254 | 0.2224 | 🔴-0.27 | 0.63 |
| S01_NAKAANA1 | win | 173 | 0.4918 | 0.2023 | 0.2493 | 🔴-0.54 | 0.656 |
| S02_TETSUBAN | win | 70 | 0.5261 | 0.5143 | 0.2415 | ✅+0.03 | 0.829 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 9 | 0.1189 | 0.1111 | ✅+0.0078 |
| 0.15-0.20 | 12 | 0.1827 | 0.0833 | 🔴+0.0994 |
| 0.20-0.30 | 8 | 0.2246 | 0.5000 | 🔴-0.2754 |
| 0.30-0.50 | 158 | 0.4193 | 0.2152 | 🔴+0.2041 |
| 0.50+ | 227 | 0.5417 | 0.3084 | 🔴+0.2333 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 109 | 0.768 |
| win | <5.0 | ✅learned | 185 | 0.736 |
| win | <10.0 | ✅learned | 95 | 0.448 |
| win | <20.0 | ✅learned | 30 | 0.227 |
| win | <50.0 | ⚠️fallback | 7 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-08-16T12:40:01.386501+09:00_