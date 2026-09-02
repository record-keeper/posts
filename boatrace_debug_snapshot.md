# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-02T09:30:01.717322+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×25 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×25 (24h)
- 🔴 CALIBRATION_DRIFT×19 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 FINAL_MISSING×5 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CALIBRATION_DRIFT  ×29  [2026-09-02T09:01:20]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×29  [2026-09-02T09:01:20]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×29  [2026-09-02T09:01:20]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×29  [2026-09-02T09:01:20]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-09-02T08:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-02T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S00: n=176<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-02T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=81<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-02T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2251 actual=0.2222 gap=+0.0029`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-02T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=8 pred=0.1250 actual=0.0000 gap=+0.1250`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-02T06:00:17]
- key: `ROI_STAT|S00: n=176 hit%=26.7% hit_CI[Bonf]=[18.3,37.2]% ROI=0.88 ROI_boot95=[0.62,1.15]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-02T06:00:17]
- key: `ROI_STAT|S01_NAKAANA1: n=193 hit%=23.3% hit_CI[Bonf]=[15.7,33.1]% ROI=0.71 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-02T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=193<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-09-02T06:00:17]
- key: `ROI_STAT|S02_TETSUBAN: n=81 hit%=40.7% hit_CI[Bonf]=[26.6,56.6]% ROI=0.70 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-09-02T06:00:17]
- key: `ORPHAN_SCAN|196 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-02T06:00:17]
- key: `DRIFT_BUCKET|drift ≤-30%: n=39 hit%=15.4% ROI=0.47 (コスト 11,300/回収 5,300)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-02T06:00:17]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=43 hit%=27.9% ROI=0.91 (コスト 10,000/回収 9,100)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-02T06:00:17]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=96 hit%=27.1% ROI=0.90 (コスト 22,000/回収 19,790)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-02T06:00:17]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=50 hit%=24.0% ROI=0.47 (コスト 11,300/回収 5,340)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-02T06:00:17]
- key: `DRIFT_BUCKET|drift ≥+30%: n=39 hit%=20.5% ROI=0.92 (コスト 10,600/回収 9,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-02T06:00:17]
- key: `CALIBRATION_LIVE|bt=win: n=450 pred=0.4736 actual=0.2778 error=+0.1959 (+41%) brier=0.2393 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 12.1MB / last modified 2026-09-02T09:30:03.789215+09:00

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
ault=5000
2026-09-02 09:26:04,171 [INFO] predictor: Models loaded OK
2026-09-02 09:26:04,278 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-02 09:27:04,159 [INFO] run_cycle: === run_cycle 09:27:04 ===
2026-09-02 09:27:04,160 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-02 09:27:04,160 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-02 09:27:04,204 [INFO] predictor: Models loaded OK
2026-09-02 09:27:04,307 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-02 09:28:04,071 [INFO] run_cycle: === run_cycle 09:28:04 ===
2026-09-02 09:28:04,071 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-02 09:28:04,071 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-02 09:28:04,127 [INFO] predictor: Models loaded OK
2026-09-02 09:28:15,568 [INFO] scraper: odds3t: 120/120 parsed
2026-09-02 09:28:16,686 [INFO] scraper: odds3f: 20/20 parsed
2026-09-02 09:28:17,766 [INFO] scraper: odds2t: 24/30 parsed
2026-09-02 09:28:17,767 [INFO] scraper: odds2f: 14/15 parsed
2026-09-02 09:28:18,863 [INFO] scraper: odds_win: 6/6 parsed
2026-09-02 09:28:18,863 [INFO] scraper: fetch_race 18/3: boats=6 odds=184/191
2026-09-02 09:28:18,867 [INFO] predictor: CALIBRATION_MODE=on
2026-09-02 09:28:18,867 [INFO] predictor: combos: {'win': 6, '2t': 24, '3t': 120}
2026-09-02 09:28:18,871 [INFO] run_cycle: fetched 18/3 [scan]: 150 combos
2026-09-02 09:28:18,986 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-02 09:29:03,978 [INFO] run_cycle: === run_cycle 09:29:03 ===
2026-09-02 09:29:03,978 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-02 09:29:03,978 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-02 09:29:04,026 [INFO] predictor: Models loaded OK
2026-09-02 09:29:04,131 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 92
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 92
  }
]
```

## Phase別通知記録 (24h)
{'final': 38, 'result': 23, 'scan': 31}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 131
  CIRCUIT_BREAKER_NO_ACTION: 31
  CIRCUIT_BREAKER_TRIP: 25
  CALIBRATION_DRIFT: 19
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 6
  FINAL_MISSING: 5
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_SCAN_FINAL_RATIO: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 49 | 12 | 14,700 | 12,630 | -2,070 | 0.859 |
| S01_NAKAANA1 | 41 | 6 | 8,200 | 3,100 | -5,100 | 0.378 |
| S02_TETSUBAN | 19 | 8 | 3,800 | 3,420 | -380 | 0.9 |

## 直近アラート (24h・新しい順)
```
[09:01:20] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[09:01:20] CIRCUIT_BREAKER_TRIP: {"cost": 8200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 41, "payout": 3100, "roi_7d": 0.378, "sid": "S01_NAKAANA1"}
[09:01:20] CALIBRATION_DRIFT: {"avg_actual": 0.2385, "avg_pred": 0.4777, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 109, "overconf_pct": 50.1}
[09:01:20] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[08:00:42] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[08:00:42] CIRCUIT_BREAKER_TRIP: {"cost": 8200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 41, "payout": 3100, "roi_7d": 0.378, "sid": "S01_NAKAANA1"}
[08:00:42] CALIBRATION_DRIFT: {"avg_actual": 0.2385, "avg_pred": 0.4777, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 109, "overconf_pct": 50.1}
[08:00:42] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[06:00:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:06] CIRCUIT_BREAKER_TRIP: {"cost": 8200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 41, "payout": 3100, "roi_7d": 0.378, "sid": "S01_NAKAANA1"}
```

## 本日残レース: 151件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 5件 締切済
- 通知発射: scan=0 nid / final=0 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 2010R | win | 1 | 0.5123 | 6.5 | 3.33 | 300 | scan=5.5 drift=+18.2% | 19:39:19 |
| S00 | 243R | win | 1 | 0.4111 | 15.6 | 6.41 | 300 | scan=- drift=- | 18:31:31 |
| S01_NAKAANA1 | 206R | win | 1 | 0.4111 | 4.1 | 1.69 | 200 | scan=4.2 drift=-2.4% | 17:33:19 |
| S01_NAKAANA1 | 124R | win | 1 | 0.4111 | 4.8 | 1.97 | 200 | scan=- drift=- | 16:27:20 |
| S01_NAKAANA1 | 193R | win | 1 | 0.4111 | 4.3 | 1.77 | 200 | scan=4.1 drift=+4.9% | 16:18:44 |
| S00 | 193R | win | 1 | 0.4111 | 4.3 | 1.77 | 300 | scan=4.1 drift=+4.9% | 16:18:43 |
| S02_TETSUBAN | 1610R | win | 1 | 0.5735 | 2.2 | 1.26 | 200 | scan=2.0 drift=+10.0% | 16:01:18 |
| S00 | 0610R | win | 1 | 0.4989 | 4.3 | 2.15 | 300 | scan=- drift=- | 15:52:19 |
| S00 | 202R | win | 1 | 0.5735 | 10.1 | 5.79 | 300 | scan=5.6 drift=+80.4% | 15:47:19 |
| S01_NAKAANA1 | 072R | win | 1 | 0.5735 | 3.9 | 2.24 | 200 | scan=4.1 drift=-4.9% | 15:41:33 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 65 | +6.8% | -73.7% | +158.3% | 18 | 9 | 44 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 501.1s |
| **Latency** (scan→final max) | 613.1s |
| **Traffic** (notifications 24h) | 92 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 450 | 0.4736 | 0.2778 | +0.1959 | 🟡+41% | 0.2393 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 176 | 0.4215 | 0.2670 | 0.2150 | 🔴-0.10 | 0.88 |
| S01_NAKAANA1 | win | 193 | 0.4894 | 0.2332 | 0.2507 | 🔴-0.40 | 0.712 |
| S02_TETSUBAN | win | 81 | 0.5495 | 0.4074 | 0.2648 | 🔴-0.10 | 0.705 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 8 | 0.1250 | 0.0000 | 🔴+0.1250 |
| 0.15-0.20 | 11 | 0.1824 | 0.1818 | ✅+0.0006 |
| 0.20-0.30 | 9 | 0.2251 | 0.2222 | ✅+0.0029 |
| 0.30-0.50 | 155 | 0.4076 | 0.2452 | 🔴+0.1624 |
| 0.50+ | 265 | 0.5463 | 0.3132 | 🔴+0.2331 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 126 | 0.778 |
| win | <5.0 | ✅learned | 228 | 0.744 |
| win | <10.0 | ✅learned | 111 | 0.458 |
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
_auto-generated by claude_snapshot.py at 2026-09-02T09:30:01.717322+09:00_