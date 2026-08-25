# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-25T13:20:02.247994+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×62 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×24 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×17  [2026-08-25T13:03:36]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×17  [2026-08-25T13:03:36]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×17  [2026-08-25T13:03:36]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-25T12:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×18  [2026-08-25T10:50:30]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

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


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 11.45MB / last modified 2026-08-25T13:19:34.489419+09:00

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
by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-25 13:19:04,452 [INFO] predictor: Models loaded OK
2026-08-25 13:19:16,832 [INFO] scraper: odds3t: 120/120 parsed
2026-08-25 13:19:17,907 [INFO] scraper: odds3f: 20/20 parsed
2026-08-25 13:19:18,996 [INFO] scraper: odds2t: 30/30 parsed
2026-08-25 13:19:18,998 [INFO] scraper: odds2f: 15/15 parsed
2026-08-25 13:19:20,092 [INFO] scraper: odds_win: 3/6 parsed
2026-08-25 13:19:20,092 [INFO] scraper: fetch_race 17/6: boats=6 odds=188/191
2026-08-25 13:19:20,096 [INFO] predictor: CALIBRATION_MODE=on
2026-08-25 13:19:20,096 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-08-25 13:19:20,100 [INFO] run_cycle: fetched 17/6 [final]: 153 combos
2026-08-25 13:19:23,769 [INFO] scraper: odds3t: 120/120 parsed
2026-08-25 13:19:24,890 [INFO] scraper: odds3f: 20/20 parsed
2026-08-25 13:19:25,966 [INFO] scraper: odds2t: 30/30 parsed
2026-08-25 13:19:25,967 [INFO] scraper: odds2f: 15/15 parsed
2026-08-25 13:19:27,070 [INFO] scraper: odds_win: 6/6 parsed
2026-08-25 13:19:27,070 [INFO] scraper: fetch_race 03/6: boats=6 odds=191/191
2026-08-25 13:19:27,072 [INFO] predictor: CALIBRATION_MODE=on
2026-08-25 13:19:27,073 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-25 13:19:27,076 [INFO] run_cycle: fetched 03/6 [scan]: 156 combos
2026-08-25 13:19:30,724 [INFO] scraper: odds3t: 120/120 parsed
2026-08-25 13:19:31,809 [INFO] scraper: odds3f: 20/20 parsed
2026-08-25 13:19:32,891 [INFO] scraper: odds2t: 30/30 parsed
2026-08-25 13:19:32,892 [INFO] scraper: odds2f: 15/15 parsed
2026-08-25 13:19:34,065 [INFO] scraper: odds_win: 6/6 parsed
2026-08-25 13:19:34,066 [INFO] scraper: fetch_race 13/7: boats=6 odds=191/191
2026-08-25 13:19:34,068 [INFO] predictor: CALIBRATION_MODE=on
2026-08-25 13:19:34,068 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-25 13:19:34,072 [INFO] run_cycle: fetched 13/7 [scan]: 156 combos
2026-08-25 13:19:34,202 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 68
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 68
  }
]
```

## Phase別通知記録 (24h)
{'final': 28, 'result': 12, 'scan': 28}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 92
  FINAL_MISSING: 62
  CIRCUIT_BREAKER_TRIP: 24
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 9
  ANOMALY_SCAN_FINAL_RATIO: 6
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 40 | 13 | 12,000 | 11,790 | -210 | 0.983 |
| S01_NAKAANA1 | 49 | 16 | 9,800 | 8,540 | -1,260 | 0.871 |
| S02_TETSUBAN | 21 | 6 | 4,200 | 2,380 | -1,820 | 0.567 |

## 直近アラート (24h・新しい順)
```
[13:18:04] CIRCUIT_BREAKER_TRIP: {"cost": 4200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 21, "payout": 2380, "roi_7d": 0.567, "sid": "S02_TETSUBAN"}
[13:03:36] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:03:36] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[12:57:50] CIRCUIT_BREAKER_TRIP: {"cost": 4400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 22, "payout": 2380, "roi_7d": 0.541, "sid": "S02_TETSUBAN"}
[12:42:26] FINAL_MISSING: {"deadline": "2026-08-25T12:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082508041212", "sid": "S00"}
[12:31:33] FINAL_MISSING: {"deadline": "2026-08-25T11:01:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082508021101", "sid": "S00"}
[12:20:46] FINAL_MISSING: {"deadline": "2026-08-25T10:49:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082521061049", "sid": "S00"}
[12:02:44] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:02:44] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[11:56:31] CIRCUIT_BREAKER_TRIP: {"cost": 4400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 22, "payout": 2380, "roi_7d": 0.541, "sid": "S02_TETSUBAN"}
```

## 本日残レース: 91件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 65件 締切済
- 通知発射: scan=12 nid / final=12 nid / result=5 nid
- predictions: 6 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 1010R | win | 1 | 0.4111 | 4.0 | 1.64 | 200 | scan=3.8 drift=+5.3% | 13:10:33 |
| S00 | 188R | win | 1 | 0.5123 | 7.8 | 4.00 | 300 | scan=6.3 drift=+23.8% | 11:57:19 |
| S01_NAKAANA1 | 133R | win | 1 | 0.4111 | 3.7 | 1.52 | 200 | scan=3.1 drift=+19.4% | 11:25:21 |
| S01_NAKAANA1 | 106R | win | 1 | 0.5174 | 3.4 | 1.76 | 200 | scan=- drift=- | 11:01:36 |
| S00 | 186R | win | 1 | 0.5735 | 4.9 | 2.81 | 300 | scan=8.8 drift=-44.3% | 10:52:29 |
| S02_TETSUBAN | 212R | win | 1 | 0.5891 | 2.4 | 1.41 | 200 | scan=- drift=- | 08:55:19 |
| S02_TETSUBAN | 209R | win | 1 | 0.5476 | 2.4 | 1.31 | 200 | scan=- drift=- | 19:06:30 |
| S02_TETSUBAN | 079R | win | 1 | 0.5334 | 2.4 | 1.28 | 200 | scan=2.5 drift=-4.0% | 18:59:18 |
| S01_NAKAANA1 | 206R | win | 1 | 0.4111 | 3.7 | 1.52 | 200 | scan=- drift=- | 17:41:18 |
| S00 | 074R | win | 1 | 0.1084 | 4.1 | 0.44 | 300 | scan=7.8 drift=-47.4% | 16:36:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 62 | +6.5% | -79.6% | +320.7% | 24 | 11 | 46 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 445.7s |
| **Latency** (scan→final max) | 672.7s |
| **Traffic** (notifications 24h) | 68 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 430 | 0.4723 | 0.2953 | +0.1769 | 🟡+38% | 0.2401 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 162 | 0.4212 | 0.2654 | 0.2236 | 🔴-0.15 | 0.819 |
| S01_NAKAANA1 | win | 187 | 0.4892 | 0.2727 | 0.2488 | 🔴-0.25 | 0.851 |
| S02_TETSUBAN | win | 81 | 0.5355 | 0.4074 | 0.2534 | 🔴-0.05 | 0.647 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 10 | 0.1249 | 0.1000 | ✅+0.0249 |
| 0.15-0.20 | 9 | 0.1799 | 0.2222 | ✅-0.0423 |
| 0.20-0.30 | 9 | 0.2251 | 0.3333 | 🔴-0.1082 |
| 0.30-0.50 | 152 | 0.4113 | 0.2303 | 🔴+0.1811 |
| 0.50+ | 249 | 0.5445 | 0.3454 | 🔴+0.1992 |

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
_auto-generated by claude_snapshot.py at 2026-08-25T13:20:02.247994+09:00_