# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-30T11:30:02.040878+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×52 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×46 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×13 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×56  [2026-05-30T11:02:41]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×56  [2026-05-30T11:02:41]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×28  [2026-05-30T11:02:41]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×6  [2026-05-30T10:44:30]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×12  [2026-05-30T10:36:34]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-05-30T10:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-05-30T10:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-30T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=26 pred=0.3234 actual=0.2308 gap=+0.0926`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-30T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=16 pred=0.0095 actual=0.0625 gap=-0.0530`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-30T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1957 actual=0.2000 gap=-0.0043`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-30T06:00:13]
- key: `ROI_STAT|S02_TETSUBAN: n=51 hit%=49.0% hit_CI[Bonf]=[30.4,67.9]% ROI=0.93 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-30T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=51<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-30T06:00:13]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=51 pred=0.5110 hit=0.4902 cal_err=+0.0208 brier=0.2555 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-30T06:00:13]
- key: `ROI_STAT|S00: n=177 hit%=27.7% hit_CI[Bonf]=[19.1,38.2]% ROI=0.94 ROI_boot95=[0.68,1.22]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-30T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S00: n=177<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-30T06:00:13]
- key: `ROI_STAT|S01_NAKAANA1: n=100 hit%=30.0% hit_CI[Bonf]=[18.7,44.3]% ROI=0.78 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-30T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=100<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-30T06:00:13]
- key: `ORPHAN_SCAN|233 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-30T06:00:13]
- key: `DRIFT_BUCKET|drift ≤-30%: n=50 hit%=32.0% ROI=0.88 (コスト 14,700/回収 12,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-30T06:00:13]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=38 hit%=28.9% ROI=1.05 (コスト 8,400/回収 8,840)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 3.82MB / last modified 2026-05-30T11:30:03.874871+09:00

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
-30 11:29:18,176 [INFO] scraper: odds3f: 20/20 parsed
2026-05-30 11:29:19,341 [INFO] scraper: odds2t: 30/30 parsed
2026-05-30 11:29:19,342 [INFO] scraper: odds2f: 15/15 parsed
2026-05-30 11:29:20,439 [INFO] scraper: odds_win: 5/6 parsed
2026-05-30 11:29:20,439 [INFO] scraper: fetch_race 14/7: boats=6 odds=190/191
2026-05-30 11:29:20,451 [INFO] predictor: CALIBRATION_MODE=on
2026-05-30 11:29:20,451 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-05-30 11:29:20,458 [INFO] run_cycle: fetched 14/7 [final]: 155 combos
2026-05-30 11:29:20,685 [INFO] race_id: notif: nid=2026053014071132 sid=S00 phase=final rank=SSS
2026-05-30 11:29:21,026 [INFO] notifier: Discord notify OK (status=204)
2026-05-30 11:29:21,620 [INFO] notifier: Discord notify OK (status=204)
2026-05-30 11:29:21,953 [INFO] run_cycle: FINAL S00 鳴門7R SSS
2026-05-30 11:29:25,508 [INFO] scraper: odds3t: 120/120 parsed
2026-05-30 11:29:26,601 [INFO] scraper: odds3f: 20/20 parsed
2026-05-30 11:29:27,709 [INFO] scraper: odds2t: 28/30 parsed
2026-05-30 11:29:27,711 [INFO] scraper: odds2f: 15/15 parsed
2026-05-30 11:29:28,791 [INFO] scraper: odds_win: 6/6 parsed
2026-05-30 11:29:28,791 [INFO] scraper: fetch_race 08/3: boats=6 odds=189/191
2026-05-30 11:29:28,801 [INFO] predictor: CALIBRATION_MODE=on
2026-05-30 11:29:28,801 [INFO] predictor: combos: {'win': 6, '2t': 28, '3t': 120}
2026-05-30 11:29:28,809 [INFO] run_cycle: fetched 08/3 [scan]: 154 combos
2026-05-30 11:29:31,168 [WARNING] scraper: beforeinfo parse failed: jcd=03 rno=2
2026-05-30 11:29:31,169 [WARNING] run_cycle: fetch None: 03/2
2026-05-30 11:29:31,169 [INFO] run_cycle: run_cycle done: 1 notifications
2026-05-30 11:30:08,484 [INFO] run_cycle: === run_cycle 11:30:08 ===
2026-05-30 11:30:08,485 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-30 11:30:08,485 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-30 11:30:08,564 [INFO] predictor: Models loaded OK

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
    "c": 64
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 64
  }
]
```

## Phase別通知記録 (24h)
{'final': 26, 'result': 15, 'scan': 23}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 80
  FINAL_MISSING: 52
  CIRCUIT_BREAKER_TRIP: 46
  CIRCUIT_BREAKER_NO_ACTION: 33
  KS_ODDS_DRIFT: 31
  STRATEGY_CI_FAIL: 17
  PSI_DRIFT_DETECTED: 13
  ANOMALY_SCAN_FINAL_RATIO: 5
  ANOMALY_BET_VOLUME_SPIKE: 3
  LARGE_ODDS_DRIFT: 2
  CRITICAL_ODDS_COLLAPSE: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 35 | 3 | 10,500 | 2,640 | -7,860 | 0.251 |
| S01_NAKAANA1 | 37 | 9 | 7,400 | 4,640 | -2,760 | 0.627 |
| S02_TETSUBAN | 11 | 7 | 2,200 | 2,880 | +680 | 1.309 |

## 直近アラート (24h・新しい順)
```
[11:29:31] CIRCUIT_BREAKER_TRIP: {"cost": 10500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 2640, "roi_7d": 0.251, "sid": "S00"}
[11:22:36] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.222, "baseline_mean": 0.794, "baseline_stdev": 0.137, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.571, "today_scan_count": 7, "z_score": -1.62}
[11:04:45] CIRCUIT_BREAKER_TRIP: {"cost": 7400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 37, "payout": 4640, "roi_7d": 0.627, "sid": "S01_NAKAANA1"}
[11:04:45] CIRCUIT_BREAKER_TRIP: {"cost": 10200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 34, "payout": 2640, "roi_7d": 0.259, "sid": "S00"}
[11:04:45] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.008899, "ks_stat": 0.205}
[11:02:41] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:02:41] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[11:02:41] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[11:00:39] CIRCUIT_BREAKER_TRIP: {"cost": 9900, "kind": "CIRCUIT_BREAKER_TRIP", "n": 33, "payout": 2640, "roi_7d": 0.267, "sid": "S00"}
[10:46:30] CIRCUIT_BREAKER_TRIP: {"cost": 9600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 32, "payout": 2640, "roi_7d": 0.275, "sid": "S00"}
```

## 本日残レース: 145件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 35件 締切済
- 通知発射: scan=7 nid / final=8 nid / result=4 nid
- predictions: 9 / うち結果DB記録済: 4
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 147R | win | 1 | 0.5990 | 11.9 | 7.13 | 300 | scan=12.3 drift=-3.3% | 11:29:20 |
| S00 | 093R | win | 1 | 0.5053 | 24.7 | 12.48 | 300 | scan=7.5 drift=+229.3% | 11:26:32 |
| S01_NAKAANA1 | 082R | win | 1 | 0.5033 | 4.7 | 2.37 | 200 | scan=- drift=- | 11:04:34 |
| S00 | 082R | win | 1 | 0.5033 | 4.7 | 2.37 | 300 | scan=- drift=- | 11:04:32 |
| S00 | 146R | win | 1 | 0.5334 | 4.5 | 2.40 | 300 | scan=- drift=- | 11:00:23 |
| S00 | 236R | win | 1 | 0.4111 | 11.5 | 4.73 | 300 | scan=7.5 drift=+53.3% | 10:46:20 |
| S01_NAKAANA1 | 021R | win | 1 | 0.5891 | 4.7 | 2.77 | 200 | scan=3.1 drift=+51.6% | 10:44:21 |
| S00 | 234R | win | 1 | 0.4111 | 7.0 | 2.88 | 300 | scan=18.0 drift=-61.1% | 09:47:22 |
| S00 | 232R | win | 1 | 0.4111 | 5.8 | 2.38 | 300 | scan=4.6 drift=+26.1% | 08:55:32 |
| S01_NAKAANA1 | 074R | win | 1 | 0.4480 | 3.7 | 1.66 | 200 | scan=- drift=- | 17:15:46 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 44 | +7.0% | -81.4% | +229.3% | 15 | 9 | 32 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 462.7s |
| **Latency** (scan→final max) | 604.9s |
| **Traffic** (notifications 24h) | 64 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,100円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 330 | 0.4553 | 0.3152 | +0.1402 | 🟡+31% | 0.2345 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 178 | 0.4219 | 0.2753 | 0.2222 | 🔴-0.11 | 0.935 |
| S01_NAKAANA1 | win | 101 | 0.4861 | 0.2970 | 0.2456 | 🔴-0.18 | 0.776 |
| S02_TETSUBAN | win | 51 | 0.5110 | 0.4902 | 0.2555 | 🔴-0.02 | 0.933 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 16 | 0.0095 | 0.0625 | 🔴-0.0530 |
| 0.10-0.15 | 5 | 0.1221 | 0.0000 | 🔴+0.1221 |
| 0.15-0.20 | 5 | 0.1957 | 0.2000 | ✅-0.0043 |
| 0.20-0.30 | 11 | 0.2239 | 0.4545 | 🔴-0.2306 |
| 0.30-0.50 | 142 | 0.4153 | 0.2746 | 🔴+0.1407 |
| 0.50+ | 161 | 0.5401 | 0.3665 | 🔴+0.1736 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 25 | 0.783 |
| win | <5.0 | ✅learned | 46 | 0.795 |
| win | <10.0 | ✅learned | 37 | 0.538 |
| win | <20.0 | ✅learned | 11 | 0.193 |
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
_auto-generated by claude_snapshot.py at 2026-05-30T11:30:02.040878+09:00_