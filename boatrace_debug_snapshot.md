# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-25T10:10:01.692928+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×23 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×61 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×23 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×7  [2026-08-25T10:02:04]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×7  [2026-08-25T10:02:04]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×7  [2026-08-25T10:02:04]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-25T09:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ORPHAN_SCAN  ×1  [2026-08-25T06:00:16]
- key: `ORPHAN_SCAN|195 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-25T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-25T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S00: n=162<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-25T06:00:16]
- key: `DRIFT_BUCKET|drift ≥+30%: n=37 hit%=21.6% ROI=0.98 (コスト 10,100/回収 9,940)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-25T06:00:16]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2251 actual=0.3333 gap=-0.1082`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-25T06:00:16]
- key: `ROI_STAT|S00: n=162 hit%=26.5% hit_CI[Bonf]=[17.9,37.5]% ROI=0.82 ROI_boot95=[0.58,1.11]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-25T06:00:16]
- key: `ROI_STAT|S01_NAKAANA1: n=187 hit%=27.3% hit_CI[Bonf]=[19.0,37.5]% ROI=0.85 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-25T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=187<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-25T06:00:16]
- key: `ROI_STAT|S02_TETSUBAN: n=80 hit%=41.2% hit_CI[Bonf]=[26.9,57.2]% ROI=0.66 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-25T06:00:16]
- key: `DRIFT_BUCKET|drift ≤-30%: n=37 hit%=18.9% ROI=0.60 (コスト 10,700/回収 6,410)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-25T06:00:16]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=40 hit%=37.5% ROI=0.99 (コスト 9,200/回収 9,090)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-25T06:00:16]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=91 hit%=29.7% ROI=0.91 (コスト 20,900/回収 19,070)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-25T06:00:16]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=49 hit%=24.5% ROI=0.51 (コスト 11,200/回収 5,730)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-25T06:00:16]
- key: `CALIBRATION_LIVE|bt=win: n=429 pred=0.4714 actual=0.2960 error=+0.1754 (+37%) brier=0.2393 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-25T06:00:16]
- key: `CALIBRATION_LIVE|S00(win): n=162 pred=0.4202 hit=0.2654 cal_err=+0.1548 brier=0.2226 BSS=-0.14 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-25T06:00:16]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=187 pred=0.4886 hit=0.2727 cal_err=+0.2159 brier=0.2482 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 11.43MB / last modified 2026-08-25T10:09:03.847525+09:00

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
2026-08-25 10:06:03,986 [INFO] predictor: Models loaded OK
2026-08-25 10:06:04,093 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-25 10:07:03,517 [INFO] run_cycle: === run_cycle 10:07:03 ===
2026-08-25 10:07:03,517 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-25 10:07:03,517 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-25 10:07:03,563 [INFO] predictor: Models loaded OK
2026-08-25 10:07:03,677 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-25 10:08:03,988 [INFO] run_cycle: === run_cycle 10:08:03 ===
2026-08-25 10:08:03,988 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-25 10:08:03,988 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-25 10:08:04,020 [INFO] predictor: Models loaded OK
2026-08-25 10:08:15,362 [INFO] scraper: odds3t: 120/120 parsed
2026-08-25 10:08:16,448 [INFO] scraper: odds3f: 20/20 parsed
2026-08-25 10:08:17,573 [INFO] scraper: odds2t: 29/30 parsed
2026-08-25 10:08:17,574 [INFO] scraper: odds2f: 12/15 parsed
2026-08-25 10:08:18,734 [INFO] scraper: odds_win: 5/6 parsed
2026-08-25 10:08:18,734 [INFO] scraper: fetch_race 21/5: boats=6 odds=186/191
2026-08-25 10:08:18,737 [INFO] predictor: CALIBRATION_MODE=on
2026-08-25 10:08:18,738 [INFO] predictor: combos: {'win': 5, '2t': 29, '3t': 120}
2026-08-25 10:08:18,741 [INFO] run_cycle: fetched 21/5 [scan]: 154 combos
2026-08-25 10:08:18,858 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-25 10:09:03,643 [INFO] run_cycle: === run_cycle 10:09:03 ===
2026-08-25 10:09:03,644 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-25 10:09:03,644 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-25 10:09:03,692 [INFO] predictor: Models loaded OK
2026-08-25 10:09:03,797 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 69
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 69
  }
]
```

## Phase別通知記録 (24h)
{'final': 29, 'result': 12, 'scan': 28}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 135
  FINAL_MISSING: 61
  CIRCUIT_BREAKER_TRIP: 23
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 9
  ANOMALY_SCAN_FINAL_RATIO: 4
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 41 | 15 | 12,300 | 16,290 | +3,990 | 1.324 |
| S01_NAKAANA1 | 51 | 18 | 10,200 | 11,680 | +1,480 | 1.145 |
| S02_TETSUBAN | 22 | 6 | 4,400 | 2,380 | -2,020 | 0.541 |

## 直近アラート (24h・新しい順)
```
[10:02:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[10:02:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[09:55:30] CIRCUIT_BREAKER_TRIP: {"cost": 4400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 22, "payout": 2380, "roi_7d": 0.541, "sid": "S02_TETSUBAN"}
[09:01:20] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[09:01:20] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[08:55:21] CIRCUIT_BREAKER_TRIP: {"cost": 4400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 22, "payout": 2380, "roi_7d": 0.541, "sid": "S02_TETSUBAN"}
[08:00:48] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[08:00:48] CIRCUIT_BREAKER_TRIP: {"cost": 4200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 21, "payout": 2380, "roi_7d": 0.567, "sid": "S02_TETSUBAN"}
[08:00:48] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[06:00:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
```

## 本日残レース: 144件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 12件 締切済
- 通知発射: scan=0 nid / final=1 nid / result=1 nid
- predictions: 1 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 212R | win | 1 | 0.5891 | 2.4 | 1.41 | 200 | scan=- drift=- | 08:55:19 |
| S02_TETSUBAN | 209R | win | 1 | 0.5476 | 2.4 | 1.31 | 200 | scan=- drift=- | 19:06:30 |
| S02_TETSUBAN | 079R | win | 1 | 0.5334 | 2.4 | 1.28 | 200 | scan=2.5 drift=-4.0% | 18:59:18 |
| S01_NAKAANA1 | 206R | win | 1 | 0.4111 | 3.7 | 1.52 | 200 | scan=- drift=- | 17:41:18 |
| S00 | 074R | win | 1 | 0.1084 | 4.1 | 0.44 | 300 | scan=7.8 drift=-47.4% | 16:36:19 |
| S00 | 1310R | win | 1 | 0.5476 | 6.4 | 3.50 | 300 | scan=- drift=- | 15:04:31 |
| S01_NAKAANA1 | 036R | win | 1 | 0.5123 | 3.9 | 2.00 | 200 | scan=4.7 drift=-17.0% | 13:26:19 |
| S01_NAKAANA1 | 1010R | win | 1 | 0.5174 | 3.1 | 1.60 | 200 | scan=- drift=- | 13:10:23 |
| S01_NAKAANA1 | 109R | win | 1 | 0.5174 | 4.0 | 2.07 | 200 | scan=4.6 drift=-13.0% | 12:37:27 |
| S01_NAKAANA1 | 188R | win | 1 | 0.4111 | 3.7 | 1.52 | 200 | scan=- drift=- | 11:57:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 64 | +6.6% | -79.6% | +320.7% | 24 | 10 | 45 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 518.4s |
| **Latency** (scan→final max) | 673.1s |
| **Traffic** (notifications 24h) | 69 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 430 | 0.4717 | 0.2953 | +0.1763 | 🟡+37% | 0.2396 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 162 | 0.4202 | 0.2654 | 0.2226 | 🔴-0.14 | 0.819 |
| S01_NAKAANA1 | win | 187 | 0.4886 | 0.2727 | 0.2482 | 🔴-0.25 | 0.851 |
| S02_TETSUBAN | win | 81 | 0.5355 | 0.4074 | 0.2534 | 🔴-0.05 | 0.647 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 10 | 0.1249 | 0.1000 | ✅+0.0249 |
| 0.15-0.20 | 9 | 0.1799 | 0.2222 | ✅-0.0423 |
| 0.20-0.30 | 9 | 0.2251 | 0.3333 | 🔴-0.1082 |
| 0.30-0.50 | 154 | 0.4113 | 0.2273 | 🔴+0.1841 |
| 0.50+ | 247 | 0.5446 | 0.3482 | 🔴+0.1964 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 118 | 0.77 |
| win | <5.0 | ✅learned | 218 | 0.748 |
| win | <10.0 | ✅learned | 103 | 0.453 |
| win | <20.0 | ✅learned | 30 | 0.227 |
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
_auto-generated by claude_snapshot.py at 2026-08-25T10:10:01.692928+09:00_