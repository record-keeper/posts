# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-27T19:30:02.351412+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×36 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×36 (24h)
- 🔴 PSI_DRIFT_DETECTED×36 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×20 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×3  [2026-05-27T19:18:24]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×25  [2026-05-27T19:05:22]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🔴 CIRCUIT_BREAKER_TRIP  ×25  [2026-05-27T19:05:22]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×25  [2026-05-27T19:05:22]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×25  [2026-05-27T19:05:22]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×25  [2026-05-27T19:05:22]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-05-27T19:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-27T06:00:09]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=27 hit%=25.9% ROI=1.03 (コスト 6,600/回収 6,780)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-27T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=16 pred=0.0095 actual=0.0625 gap=-0.0530`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-27T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1957 actual=0.2000 gap=-0.0043`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-27T06:00:09]
- key: `ROI_STAT|S00: n=181 hit%=27.6% hit_CI[Bonf]=[19.2,38.0]% ROI=0.92 ROI_boot95=[0.66,1.21]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-27T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S00: n=181<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-27T06:00:09]
- key: `ROI_STAT|S01_NAKAANA1: n=83 hit%=28.9% hit_CI[Bonf]=[17.0,44.7]% ROI=0.77 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-27T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=83<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-27T06:00:09]
- key: `ROI_STAT|S02_TETSUBAN: n=46 hit%=47.8% hit_CI[Bonf]=[28.6,67.7]% ROI=0.88 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-27T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=46<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-27T06:00:09]
- key: `ORPHAN_SCAN|232 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-27T06:00:09]
- key: `DRIFT_BUCKET|drift ≤-30%: n=50 hit%=34.0% ROI=0.91 (コスト 14,800/回収 13,440)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-27T06:00:09]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=39 hit%=28.2% ROI=0.99 (コスト 8,900/回収 8,840)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-27T06:00:09]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=63 hit%=28.6% ROI=0.88 (コスト 15,100/回収 13,320)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 3.58MB / last modified 2026-05-27T19:30:04.376151+09:00

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
:32,176 [INFO] run_cycle: fetched 15/10 [final]: 156 combos
2026-05-27 19:28:35,929 [INFO] scraper: odds3t: 120/120 parsed
2026-05-27 19:28:37,058 [INFO] scraper: odds3f: 20/20 parsed
2026-05-27 19:28:38,161 [INFO] scraper: odds2t: 30/30 parsed
2026-05-27 19:28:38,162 [INFO] scraper: odds2f: 15/15 parsed
2026-05-27 19:28:39,248 [INFO] scraper: odds_win: 6/6 parsed
2026-05-27 19:28:39,248 [INFO] scraper: fetch_race 24/10: boats=6 odds=191/191
2026-05-27 19:28:39,256 [INFO] predictor: CALIBRATION_MODE=on
2026-05-27 19:28:39,256 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-27 19:28:39,264 [INFO] run_cycle: fetched 24/10 [scan]: 156 combos
2026-05-27 19:28:39,367 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-27 19:29:06,092 [INFO] run_cycle: === run_cycle 19:29:06 ===
2026-05-27 19:29:06,092 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-27 19:29:06,092 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-27 19:29:06,158 [INFO] predictor: Models loaded OK
2026-05-27 19:29:17,206 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=10&jcd=15&hd=20260527: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-05-27 19:29:29,563 [INFO] scraper: odds3t: 120/120 parsed
2026-05-27 19:29:30,702 [INFO] scraper: odds3f: 20/20 parsed
2026-05-27 19:29:32,004 [INFO] scraper: odds2t: 30/30 parsed
2026-05-27 19:29:32,005 [INFO] scraper: odds2f: 15/15 parsed
2026-05-27 19:29:33,146 [INFO] scraper: odds_win: 6/6 parsed
2026-05-27 19:29:33,147 [INFO] scraper: fetch_race 15/10: boats=6 odds=191/191
2026-05-27 19:29:33,158 [INFO] predictor: CALIBRATION_MODE=on
2026-05-27 19:29:33,158 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-27 19:29:33,166 [INFO] run_cycle: fetched 15/10 [final]: 156 combos
2026-05-27 19:29:33,396 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 36
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 36
  }
]
```

## Phase別通知記録 (24h)
{'final': 15, 'result': 5, 'scan': 16}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 36
  PSI_DRIFT_DETECTED: 36
  CIRCUIT_BREAKER_TRIP: 20
  CIRCUIT_BREAKER_NO_ACTION: 18
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 14
  ANOMALY_SCAN_FINAL_RATIO: 5
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 32 | 10 | 9,600 | 10,050 | +450 | 1.047 |
| S01_NAKAANA1 | 28 | 6 | 5,600 | 2,840 | -2,760 | 0.507 |
| S02_TETSUBAN | 13 | 8 | 2,600 | 3,280 | +680 | 1.262 |

## 直近アラート (24h・新しい順)
```
[19:28:39] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 235, "n_recent": 73, "psi": 0.548}
[19:27:05] CIRCUIT_BREAKER_TRIP: {"cost": 5600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 28, "payout": 2840, "roi_7d": 0.507, "sid": "S01_NAKAANA1"}
[19:18:24] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.227, "baseline_mean": 0.852, "baseline_stdev": 0.143, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.625, "today_scan_count": 16, "z_score": -1.59}
[19:17:21] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 236, "n_recent": 73, "psi": 0.547}
[19:13:05] FINAL_MISSING: {"deadline": "2026-05-27T17:43:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052707051743", "sid": "S00"}
[19:05:22] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[19:05:22] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[19:00:10] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 11.3, "baseline_n_days": 7, "baseline_stdev": 2.8, "hour": 19, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 5, "z_score": -2.24}
[18:55:41] FINAL_MISSING: {"deadline": "2026-05-27T17:24:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052715051724", "sid": "S00"}
[18:48:22] FINAL_MISSING: {"deadline": "2026-05-27T09:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052721020912", "sid": "S00"}
```

## 本日残レース: 12件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 132件 締切済
- 通知発射: scan=16 nid / final=14 nid / result=4 nid
- predictions: 5 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 074R | win | 1 | 0.4111 | 5.7 | 2.34 | 300 | scan=- drift=- | 17:15:21 |
| S00 | 073R | win | 1 | 0.4111 | 6.0 | 2.47 | 300 | scan=- drift=- | 16:45:31 |
| S02_TETSUBAN | 073R | win | 1 | 0.4111 | 2.8 | 1.15 | 200 | scan=2.4 drift=+16.7% | 16:44:32 |
| S02_TETSUBAN | 2111R | win | 1 | 0.5334 | 2.0 | 1.07 | 200 | scan=- drift=- | 13:32:22 |
| S02_TETSUBAN | 032R | win | 1 | 0.4989 | 2.3 | 1.15 | 200 | scan=- drift=- | 11:38:20 |
| S00 | 127R | win | 1 | 0.2173 | 9.8 | 2.13 | 300 | scan=- drift=- | 18:24:21 |
| S01_NAKAANA1 | 123R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=4.1 drift=-24.4% | 16:39:32 |
| S00 | 152R | win | 1 | 0.4111 | 11.2 | 4.60 | 300 | scan=7.5 drift=+49.3% | 15:47:21 |
| S01_NAKAANA1 | 1010R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=- drift=- | 12:51:22 |
| S00 | 109R | win | 1 | 0.3177 | 12.9 | 4.10 | 300 | scan=19.1 drift=-32.5% | 12:19:32 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 42 | -1.3% | -78.6% | +157.5% | 17 | 10 | 32 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 433.8s |
| **Latency** (scan→final max) | 610.5s |
| **Traffic** (notifications 24h) | 36 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 308 | 0.4536 | 0.3214 | +0.1322 | 🟡+29% | 0.2343 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 176 | 0.4240 | 0.2898 | 0.2224 | 🔴-0.08 | 0.972 |
| S01_NAKAANA1 | win | 83 | 0.4839 | 0.2892 | 0.2471 | 🔴-0.20 | 0.767 |
| S02_TETSUBAN | win | 49 | 0.5085 | 0.4898 | 0.2555 | 🔴-0.02 | 0.945 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 16 | 0.0095 | 0.0625 | 🔴-0.0530 |
| 0.15-0.20 | 5 | 0.1957 | 0.2000 | ✅-0.0043 |
| 0.20-0.30 | 12 | 0.2234 | 0.4167 | 🔴-0.1933 |
| 0.30-0.50 | 138 | 0.4171 | 0.2826 | 🔴+0.1345 |
| 0.50+ | 144 | 0.5400 | 0.3750 | 🔴+0.1650 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 24 | 0.792 |
| win | <5.0 | ✅learned | 40 | 0.808 |
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
_auto-generated by claude_snapshot.py at 2026-05-27T19:30:02.351412+09:00_