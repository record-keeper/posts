# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-12T10:10:01.653216+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×60 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×63 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×60 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×12 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×18  [2026-06-12T10:01:25]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×27  [2026-06-12T10:01:25]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×9  [2026-06-12T10:01:25]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-12T10:00:06]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-12T10:00:06]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-12T10:00:06]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-12T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1254 actual=0.1667 gap=-0.0412`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-12T06:00:13]
- key: `ROI_STAT|S00: n=150 hit%=28.7% hit_CI[Bonf]=[19.4,40.2]% ROI=0.85 ROI_boot95=[0.59,1.14]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-12T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S00: n=150<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-12T06:00:13]
- key: `ROI_STAT|S01_NAKAANA1: n=134 hit%=26.9% hit_CI[Bonf]=[17.4,39.0]% ROI=0.70 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-12T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=134<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-12T06:00:13]
- key: `ROI_STAT|S02_TETSUBAN: n=82 hit%=34.1% hit_CI[Bonf]=[21.1,50.1]% ROI=0.57 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-12T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=82<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-06-12T06:00:13]
- key: `ORPHAN_SCAN|143 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-12T06:00:13]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=34.3% ROI=1.00 (コスト 10,300/回収 10,290)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-12T06:00:13]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=35 hit%=17.1% ROI=0.35 (コスト 7,700/回収 2,710)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-12T06:00:13]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=70 hit%=28.6% ROI=0.57 (コスト 16,500/回収 9,420)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-12T06:00:13]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=35 hit%=20.0% ROI=0.72 (コスト 7,900/回収 5,660)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-12T06:00:13]
- key: `DRIFT_BUCKET|drift ≥+30%: n=31 hit%=19.4% ROI=0.49 (コスト 8,500/回収 4,170)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-12T06:00:13]
- key: `CALIBRATION_LIVE|bt=win: n=366 pred=0.4696 actual=0.2923 error=+0.1773 (+38%) brier=0.2372 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 4.88MB / last modified 2026-06-12T10:09:22.286057+09:00

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
06-12 10:06:22,010 [INFO] run_cycle: fetched 10/5 [scan]: 153 combos
2026-06-12 10:06:22,120 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-12 10:07:06,517 [INFO] run_cycle: === run_cycle 10:07:06 ===
2026-06-12 10:07:06,517 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-12 10:07:06,517 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-12 10:07:06,576 [INFO] predictor: Models loaded OK
2026-06-12 10:07:06,678 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-12 10:08:06,131 [INFO] run_cycle: === run_cycle 10:08:06 ===
2026-06-12 10:08:06,131 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-12 10:08:06,131 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-12 10:08:06,193 [INFO] predictor: Models loaded OK
2026-06-12 10:08:06,302 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-12 10:09:05,692 [INFO] run_cycle: === run_cycle 10:09:05 ===
2026-06-12 10:09:05,692 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-12 10:09:05,692 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-12 10:09:05,742 [INFO] predictor: Models loaded OK
2026-06-12 10:09:18,137 [INFO] scraper: odds3t: 120/120 parsed
2026-06-12 10:09:19,219 [INFO] scraper: odds3f: 20/20 parsed
2026-06-12 10:09:20,303 [INFO] scraper: odds2t: 30/30 parsed
2026-06-12 10:09:20,305 [INFO] scraper: odds2f: 15/15 parsed
2026-06-12 10:09:21,384 [INFO] scraper: odds_win: 5/6 parsed
2026-06-12 10:09:21,384 [INFO] scraper: fetch_race 10/5: boats=6 odds=190/191
2026-06-12 10:09:21,397 [INFO] predictor: CALIBRATION_MODE=on
2026-06-12 10:09:21,397 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-06-12 10:09:21,404 [INFO] run_cycle: fetched 10/5 [scan]: 155 combos
2026-06-12 10:09:21,509 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 35, 'result': 20, 'scan': 37}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 64
  FINAL_MISSING: 63
  CIRCUIT_BREAKER_TRIP: 60
  CIRCUIT_BREAKER_NO_ACTION: 51
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 12
  CALIBRATION_DRIFT: 12
  ANOMALY_SCAN_FINAL_RATIO: 5
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 13 | 12,600 | 10,320 | -2,280 | 0.819 |
| S01_NAKAANA1 | 32 | 9 | 6,400 | 4,100 | -2,300 | 0.641 |
| S02_TETSUBAN | 26 | 6 | 5,200 | 1,840 | -3,360 | 0.354 |

## 直近アラート (24h・新しい順)
```
[10:01:25] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[10:01:25] CIRCUIT_BREAKER_TRIP: {"cost": 5200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 26, "payout": 1840, "roi_7d": 0.354, "sid": "S02_TETSUBAN"}
[10:01:25] CIRCUIT_BREAKER_TRIP: {"cost": 6400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 32, "payout": 4100, "roi_7d": 0.641, "sid": "S01_NAKAANA1"}
[10:01:25] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[10:01:25] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[10:01:25] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[09:40:24] CIRCUIT_BREAKER_TRIP: {"cost": 6200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 31, "payout": 4100, "roi_7d": 0.661, "sid": "S01_NAKAANA1"}
[09:09:22] CIRCUIT_BREAKER_TRIP: {"cost": 6200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 31, "payout": 3720, "roi_7d": 0.6, "sid": "S01_NAKAANA1"}
[09:01:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[09:01:05] CIRCUIT_BREAKER_TRIP: {"cost": 5200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 26, "payout": 1840, "roi_7d": 0.354, "sid": "S02_TETSUBAN"}
```

## 本日残レース: 132件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 12件 締切済
- 通知発射: scan=2 nid / final=3 nid / result=1 nid
- predictions: 2 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 144R | win | 1 | 0.3177 | 3.3 | 1.05 | 200 | scan=3.1 drift=+6.5% | 10:01:22 |
| S01_NAKAANA1 | 142R | win | 1 | 0.5123 | 3.3 | 1.69 | 200 | scan=- drift=- | 09:09:20 |
| S02_TETSUBAN | 2010R | win | 1 | 0.5334 | 2.2 | 1.17 | 200 | scan=- drift=- | 19:39:22 |
| S00 | 075R | win | 1 | 0.5123 | 6.2 | 3.18 | 300 | scan=36.3 drift=-82.9% | 17:39:22 |
| S00 | 073R | win | 1 | 0.5334 | 9.0 | 4.80 | 300 | scan=4.8 drift=+87.5% | 16:38:21 |
| S02_TETSUBAN | 1610R | win | 1 | 0.5334 | 2.5 | 1.33 | 200 | scan=2.5 drift=+0.0% | 15:34:34 |
| S00 | 201R | win | 1 | 0.5334 | 5.4 | 2.88 | 300 | scan=5.5 drift=-1.8% | 15:22:24 |
| S02_TETSUBAN | 036R | win | 1 | 0.5891 | 2.4 | 1.41 | 200 | scan=- drift=- | 13:27:20 |
| S00 | 035R | win | 1 | 0.5891 | 6.0 | 3.53 | 300 | scan=6.0 drift=+0.0% | 12:59:31 |
| S00 | 053R | win | 1 | 0.4111 | 9.4 | 3.86 | 300 | scan=15.8 drift=-40.5% | 12:29:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 59 | +6.1% | -82.9% | +274.6% | 19 | 9 | 32 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 468.0s |
| **Latency** (scan→final max) | 616.2s |
| **Traffic** (notifications 24h) | 92 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 367 | 0.4697 | 0.2943 | +0.1755 | 🟡+37% | 0.2372 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 150 | 0.4195 | 0.2867 | 0.2163 | 🔴-0.06 | 0.849 |
| S01_NAKAANA1 | win | 135 | 0.4886 | 0.2741 | 0.2442 | 🔴-0.23 | 0.713 |
| S02_TETSUBAN | win | 82 | 0.5305 | 0.3415 | 0.2636 | 🔴-0.17 | 0.567 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1254 | 0.1667 | ✅-0.0412 |
| 0.15-0.20 | 5 | 0.1835 | 0.2000 | ✅-0.0165 |
| 0.20-0.30 | 6 | 0.2236 | 0.3333 | 🔴-0.1097 |
| 0.30-0.50 | 136 | 0.4212 | 0.2279 | 🔴+0.1932 |
| 0.50+ | 206 | 0.5420 | 0.3544 | 🔴+0.1876 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 37 | 0.733 |
| win | <5.0 | ✅learned | 70 | 0.715 |
| win | <10.0 | ✅learned | 46 | 0.501 |
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
_auto-generated by claude_snapshot.py at 2026-06-12T10:10:01.653216+09:00_