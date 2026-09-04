# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-04T13:50:01.784882+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×72 (24h)
- 🔴 PSI_DRIFT_DETECTED×48 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×21 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×6 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×46  [2026-09-04T13:04:27]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×46  [2026-09-04T13:04:27]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×46  [2026-09-04T13:04:27]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×46  [2026-09-04T13:04:27]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CALIBRATION_DRIFT  ×49  [2026-09-04T13:01:21]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-09-04T13:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×5  [2026-09-04T11:32:37]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ORPHAN_SCAN  ×1  [2026-09-04T06:00:14]
- key: `ORPHAN_SCAN|192 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=183<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=81<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-04T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=10 pred=0.1791 actual=0.2000 gap=-0.0209`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=188<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-04T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2251 actual=0.2222 gap=+0.0029`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-04T06:00:14]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=43 hit%=27.9% ROI=0.90 (コスト 10,100/回収 9,100)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-04T06:00:14]
- key: `DRIFT_BUCKET|drift ≥+30%: n=41 hit%=19.5% ROI=0.87 (コスト 11,200/回収 9,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-04T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=115 pred=0.4375 actual=0.2261 gap=+0.2114`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-04T06:00:14]
- key: `ROI_STAT|S00: n=183 hit%=27.9% hit_CI[Bonf]=[19.4,38.2]% ROI=0.95 ROI_boot95=[0.69,1.23]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-04T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=188 hit%=23.9% hit_CI[Bonf]=[16.2,33.9]% ROI=0.74 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-04T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=81 hit%=39.5% hit_CI[Bonf]=[25.5,55.4]% ROI=0.67 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-04T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=17.1% ROI=0.52 (コスト 10,100/回収 5,300)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 12.29MB / last modified 2026-09-04T13:49:43.890380+09:00

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
l]: 156 combos
2026-09-04 13:47:19,478 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-04 13:48:03,837 [INFO] run_cycle: === run_cycle 13:48:03 ===
2026-09-04 13:48:03,837 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-04 13:48:03,837 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-04 13:48:03,872 [INFO] predictor: Models loaded OK
2026-09-04 13:48:04,127 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-04 13:49:03,782 [INFO] run_cycle: === run_cycle 13:49:03 ===
2026-09-04 13:49:03,782 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-04 13:49:03,782 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-04 13:49:03,828 [INFO] predictor: Models loaded OK
2026-09-04 13:49:14,871 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=5&jcd=22&hd=20260904: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-09-04 13:49:25,903 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=5&jcd=22&hd=20260904: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-09-04 13:49:40,320 [INFO] scraper: odds3t: 120/120 parsed
2026-09-04 13:49:41,409 [INFO] scraper: odds3f: 20/20 parsed
2026-09-04 13:49:42,530 [INFO] scraper: odds2t: 30/30 parsed
2026-09-04 13:49:42,531 [INFO] scraper: odds2f: 15/15 parsed
2026-09-04 13:49:43,608 [INFO] scraper: odds_win: 4/6 parsed
2026-09-04 13:49:43,609 [INFO] scraper: fetch_race 22/5: boats=6 odds=189/191
2026-09-04 13:49:43,613 [INFO] predictor: CALIBRATION_MODE=on
2026-09-04 13:49:43,613 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-09-04 13:49:43,617 [INFO] run_cycle: fetched 22/5 [scan]: 154 combos
2026-09-04 13:49:43,746 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 58
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 58
  }
]
```

## Phase別通知記録 (24h)
{'final': 22, 'result': 12, 'scan': 24}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 72
  ANOMALY_SCRAPER_FAILURE_BURST: 69
  PSI_DRIFT_DETECTED: 48
  ANOMALY_SCAN_FINAL_RATIO: 21
  CIRCUIT_BREAKER_TRIP: 21
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  CALIBRATION_DRIFT: 6
  ANOMALY_BET_VOLUME_DROP: 1
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 47 | 13 | 14,100 | 13,020 | -1,080 | 0.923 |
| S01_NAKAANA1 | 34 | 3 | 6,800 | 1,560 | -5,240 | 0.229 |
| S02_TETSUBAN | 14 | 5 | 2,800 | 2,000 | -800 | 0.714 |

## 直近アラート (24h・新しい順)
```
[13:42:27] CALIBRATION_DRIFT: {"avg_actual": 0.2258, "avg_pred": 0.4755, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 93, "overconf_pct": 52.5}
[13:42:27] FINAL_MISSING: {"deadline": "2026-09-04T12:11:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090417031211", "sid": "S00"}
[13:41:20] CIRCUIT_BREAKER_TRIP: {"cost": 6800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 34, "payout": 1560, "roi_7d": 0.229, "sid": "S01_NAKAANA1"}
[13:41:20] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 359, "n_recent": 95, "psi": 0.337}
[13:40:30] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 359, "n_recent": 94, "psi": 0.337}
[13:28:27] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 359, "n_recent": 93, "psi": 0.337}
[13:12:57] CALIBRATION_DRIFT: {"avg_actual": 0.2283, "avg_pred": 0.4772, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 92, "overconf_pct": 52.2}
[13:11:34] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 360, "n_recent": 93, "psi": 0.336}
[13:04:26] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:04:26] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
```

## 本日残レース: 91件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 65件 締切済
- 通知発射: scan=12 nid / final=12 nid / result=7 nid
- predictions: 9 / うち結果DB記録済: 7
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 176R | win | 1 | 0.5174 | 3.4 | 1.76 | 200 | scan=- drift=- | 13:41:18 |
| S00 | 176R | win | 1 | 0.5174 | 6.3 | 3.26 | 300 | scan=6.0 drift=+5.0% | 13:40:21 |
| S00 | 026R | win | 1 | 0.3177 | 6.5 | 2.07 | 300 | scan=6.6 drift=-1.5% | 13:11:31 |
| S01_NAKAANA1 | 025R | win | 1 | 0.5588 | 3.8 | 2.12 | 200 | scan=3.3 drift=+15.2% | 12:41:30 |
| S00 | 024R | win | 1 | 0.4111 | 6.7 | 2.75 | 300 | scan=12.0 drift=-44.2% | 12:11:25 |
| S00 | 108R | win | 1 | 0.5044 | 5.1 | 2.57 | 300 | scan=5.6 drift=-8.9% | 11:49:43 |
| S01_NAKAANA1 | 172R | win | 1 | 0.4111 | 4.1 | 1.69 | 200 | scan=3.0 drift=+36.7% | 11:37:30 |
| S01_NAKAANA1 | 106R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=3.0 drift=+20.0% | 10:47:19 |
| S00 | 102R | win | 1 | 0.5891 | 6.4 | 3.77 | 300 | scan=- drift=- | 08:55:19 |
| S02_TETSUBAN | 1611R | win | 1 | 0.5174 | 2.8 | 1.45 | 200 | scan=- drift=- | 16:42:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 54 | +11.0% | -73.7% | +158.3% | 11 | 7 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 420.7s |
| **Latency** (scan→final max) | 611.1s |
| **Traffic** (notifications 24h) | 58 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 452 | 0.4734 | 0.2765 | +0.1969 | 🟡+42% | 0.2408 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 184 | 0.4240 | 0.2772 | 0.2205 | 🔴-0.10 | 0.934 |
| S01_NAKAANA1 | win | 188 | 0.4891 | 0.2287 | 0.2500 | 🔴-0.42 | 0.717 |
| S02_TETSUBAN | win | 80 | 0.5502 | 0.3875 | 0.2654 | 🔴-0.12 | 0.667 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1266 | 0.0000 | 🔴+0.1266 |
| 0.15-0.20 | 10 | 0.1791 | 0.2000 | ✅-0.0209 |
| 0.20-0.30 | 9 | 0.2251 | 0.2222 | ✅+0.0029 |
| 0.30-0.50 | 160 | 0.4065 | 0.2375 | 🔴+0.1690 |
| 0.50+ | 264 | 0.5461 | 0.3106 | 🔴+0.2355 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 127 | 0.776 |
| win | <5.0 | ✅learned | 232 | 0.741 |
| win | <10.0 | ✅learned | 115 | 0.468 |
| win | <20.0 | ✅learned | 31 | 0.231 |
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
_auto-generated by claude_snapshot.py at 2026-09-04T13:50:01.784882+09:00_