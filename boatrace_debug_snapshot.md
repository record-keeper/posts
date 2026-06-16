# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-16T10:40:02.378223+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×18 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×32 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×18 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×39  [2026-06-16T10:01:23]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×39  [2026-06-16T10:01:23]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×39  [2026-06-16T10:01:23]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-06-16T09:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-16T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=134<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-16T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1835 actual=0.2000 gap=-0.0165`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-16T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=21 pred=0.3200 actual=0.3333 gap=-0.0134`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-16T06:00:12]
- key: `ROI_STAT|S01_NAKAANA1: n=134 hit%=29.1% hit_CI[Bonf]=[19.3,41.4]% ROI=0.86 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-16T06:00:12]
- key: `ROI_STAT|S02_TETSUBAN: n=79 hit%=35.4% hit_CI[Bonf]=[22.0,51.7]% ROI=0.58 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-16T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=79<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-16T06:00:12]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=31 hit%=16.1% ROI=0.28 (コスト 6,800/回収 1,900)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-16T06:00:12]
- key: `DRIFT_BUCKET|drift ≥+30%: n=29 hit%=20.7% ROI=0.48 (コスト 8,000/回収 3,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-16T06:00:12]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=79 pred=0.5344 hit=0.3544 cal_err=+0.1800 brier=0.2647 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-16T06:00:12]
- key: `ROI_STAT|S00: n=143 hit%=28.0% hit_CI[Bonf]=[18.6,39.8]% ROI=0.86 ROI_boot95=[0.60,1.16]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-16T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S00: n=143<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-06-16T06:00:12]
- key: `ORPHAN_SCAN|134 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-16T06:00:12]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=27.3% ROI=0.82 (コスト 9,600/回収 7,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-16T06:00:12]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=67 hit%=31.3% ROI=0.69 (コスト 15,800/回収 10,970)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-16T06:00:12]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=37 hit%=18.9% ROI=0.97 (コスト 8,400/回収 8,140)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-16T06:00:12]
- key: `CALIBRATION_LIVE|bt=win: n=356 pred=0.4710 actual=0.3006 error=+0.1705 (+36%) brier=0.2403 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 5.16MB / last modified 2026-06-16T10:39:28.013946+09:00

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
2026-06-16 10:38:28,496 [INFO] scraper: fetch_race 16/1: boats=6 odds=187/191
2026-06-16 10:38:28,505 [INFO] predictor: CALIBRATION_MODE=on
2026-06-16 10:38:28,505 [INFO] predictor: combos: {'win': 2, '2t': 30, '3t': 120}
2026-06-16 10:38:28,512 [INFO] run_cycle: fetched 16/1 [scan]: 152 combos
2026-06-16 10:38:28,618 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-16 10:39:05,910 [INFO] run_cycle: === run_cycle 10:39:05 ===
2026-06-16 10:39:05,910 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-16 10:39:05,910 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-16 10:39:05,981 [INFO] predictor: Models loaded OK
2026-06-16 10:39:17,386 [INFO] scraper: odds3t: 120/120 parsed
2026-06-16 10:39:18,530 [INFO] scraper: odds3f: 20/20 parsed
2026-06-16 10:39:19,682 [INFO] scraper: odds2t: 30/30 parsed
2026-06-16 10:39:19,683 [INFO] scraper: odds2f: 15/15 parsed
2026-06-16 10:39:20,771 [INFO] scraper: odds_win: 6/6 parsed
2026-06-16 10:39:20,771 [INFO] scraper: fetch_race 09/1: boats=6 odds=191/191
2026-06-16 10:39:20,784 [INFO] predictor: CALIBRATION_MODE=on
2026-06-16 10:39:20,784 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-16 10:39:20,792 [INFO] run_cycle: fetched 09/1 [final]: 156 combos
2026-06-16 10:39:24,249 [INFO] scraper: odds3t: 120/120 parsed
2026-06-16 10:39:25,384 [INFO] scraper: odds3f: 20/20 parsed
2026-06-16 10:39:26,518 [INFO] scraper: odds2t: 30/30 parsed
2026-06-16 10:39:26,519 [INFO] scraper: odds2f: 15/15 parsed
2026-06-16 10:39:27,591 [INFO] scraper: odds_win: 6/6 parsed
2026-06-16 10:39:27,591 [INFO] scraper: fetch_race 21/6: boats=6 odds=191/191
2026-06-16 10:39:27,599 [INFO] predictor: CALIBRATION_MODE=on
2026-06-16 10:39:27,599 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-16 10:39:27,607 [INFO] run_cycle: fetched 21/6 [scan]: 156 combos
2026-06-16 10:39:27,967 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 35
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 35
  }
]
```

## Phase別通知記録 (24h)
{'final': 14, 'result': 6, 'scan': 15}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 131
  FINAL_MISSING: 32
  CIRCUIT_BREAKER_TRIP: 18
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 3
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 37 | 16 | 11,100 | 14,250 | +3,150 | 1.284 |
| S01_NAKAANA1 | 30 | 13 | 6,000 | 8,300 | +2,300 | 1.383 |
| S02_TETSUBAN | 21 | 7 | 4,200 | 2,060 | -2,140 | 0.49 |

## 直近アラート (24h・新しい順)
```
[10:01:22] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[10:01:22] CIRCUIT_BREAKER_TRIP: {"cost": 4200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 21, "payout": 2060, "roi_7d": 0.49, "sid": "S02_TETSUBAN"}
[10:01:22] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[09:01:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[09:01:05] CIRCUIT_BREAKER_TRIP: {"cost": 4200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 21, "payout": 2060, "roi_7d": 0.49, "sid": "S02_TETSUBAN"}
[09:01:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[08:00:45] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[08:00:45] CIRCUIT_BREAKER_TRIP: {"cost": 4200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 21, "payout": 2060, "roi_7d": 0.49, "sid": "S02_TETSUBAN"}
[08:00:45] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[06:00:07] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
```

## 本日残レース: 128件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 16件 締切済
- 通知発射: scan=1 nid / final=2 nid / result=1 nid
- predictions: 1 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 103R | win | 1 | 0.5123 | 3.2 | 1.64 | 200 | scan=- drift=- | 09:28:20 |
| S01_NAKAANA1 | 012R | win | 1 | 0.2290 | 4.8 | 1.10 | 200 | scan=3.7 drift=+29.7% | 15:54:23 |
| S00 | 012R | win | 1 | 0.2290 | 4.8 | 1.10 | 300 | scan=4.5 drift=+6.7% | 15:54:21 |
| S01_NAKAANA1 | 224R | win | 1 | 0.5476 | 3.1 | 1.70 | 200 | scan=3.9 drift=-20.5% | 13:54:27 |
| S01_NAKAANA1 | 065R | win | 1 | 0.4111 | 3.3 | 1.36 | 200 | scan=3.0 drift=+10.0% | 13:42:23 |
| S00 | 109R | win | 1 | 0.4111 | 7.2 | 2.96 | 300 | scan=- drift=- | 12:25:21 |
| S00 | 127R | win | 1 | 0.5476 | 5.4 | 2.96 | 300 | scan=9.2 drift=-41.3% | 18:18:20 |
| S01_NAKAANA1 | 014R | win | 1 | 0.4111 | 4.0 | 1.64 | 200 | scan=4.5 drift=-11.1% | 17:10:25 |
| S00 | 012R | win | 1 | 0.5174 | 16.1 | 8.33 | 300 | scan=- drift=- | 15:52:22 |
| S02_TETSUBAN | 201R | win | 1 | 0.5334 | 2.8 | 1.49 | 200 | scan=- drift=- | 15:15:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 52 | -0.3% | -82.9% | +162.5% | 17 | 9 | 29 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 435.8s |
| **Latency** (scan→final max) | 594.1s |
| **Traffic** (notifications 24h) | 35 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 356 | 0.4710 | 0.3006 | +0.1705 | 🟡+36% | 0.2403 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 143 | 0.4233 | 0.2797 | 0.2226 | 🔴-0.11 | 0.862 |
| S01_NAKAANA1 | win | 134 | 0.4846 | 0.2910 | 0.2446 | 🔴-0.19 | 0.837 |
| S02_TETSUBAN | win | 79 | 0.5344 | 0.3544 | 0.2647 | 🔴-0.16 | 0.582 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 5 | 0.1835 | 0.2000 | ✅-0.0165 |
| 0.20-0.30 | 9 | 0.2254 | 0.2222 | ✅+0.0032 |
| 0.30-0.50 | 125 | 0.4191 | 0.2480 | 🔴+0.1711 |
| 0.50+ | 206 | 0.5410 | 0.3495 | 🔴+0.1914 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 41 | 0.721 |
| win | <5.0 | ✅learned | 78 | 0.755 |
| win | <10.0 | ✅learned | 51 | 0.498 |
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
_auto-generated by claude_snapshot.py at 2026-06-16T10:40:02.378223+09:00_