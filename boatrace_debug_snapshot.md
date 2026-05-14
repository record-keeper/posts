# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-14T22:40:01.407413+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×31 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×79 (24h)
- 🔴 PSI_DRIFT_DETECTED×31 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 PSI_DRIFT_DETECTED  ×33  [2026-05-14T22:07:08]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×33  [2026-05-14T22:07:08]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×33  [2026-05-14T22:07:08]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×52  [2026-05-14T13:49:13]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×9  [2026-05-14T11:14:32]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-14T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=13 pred=0.0030 actual=0.0769 gap=-0.0739`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-14T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1907 actual=0.1429 gap=+0.0479`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-14T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2234 actual=0.3000 gap=-0.0766`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-14T06:00:12]
- key: `ROI_STAT|S00: n=176 hit%=25.6% hit_CI[Bonf]=[17.3,36.0]% ROI=0.87 ROI_boot95=[0.62,1.14]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-14T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S00: n=176<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-14T06:00:12]
- key: `ROI_STAT|S01_NAKAANA1: n=30 hit%=43.3% hit_CI[Bonf]=[21.6,67.9]% ROI=0.87 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-14T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=30<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-14T06:00:12]
- key: `ORPHAN_SCAN|212 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-14T06:00:12]
- key: `DRIFT_BUCKET|drift ≤-30%: n=39 hit%=20.5% ROI=0.58 (コスト 11,500/回収 6,660)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-14T06:00:12]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=28 hit%=32.1% ROI=1.51 (コスト 6,800/回収 10,260)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-14T06:00:12]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=45 hit%=28.9% ROI=1.04 (コスト 11,400/回収 11,840)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-14T06:00:12]
- key: `DRIFT_BUCKET|drift ≥+30%: n=31 hit%=22.6% ROI=0.64 (コスト 8,300/回収 5,280)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-14T06:00:12]
- key: `CALIBRATION_LIVE|bt=win: n=226 pred=0.4505 actual=0.3009 error=+0.1496 (+33%) brier=0.2316 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-14T06:00:12]
- key: `CALIBRATION_LIVE|S00(win): n=176 pred=0.4372 hit=0.2557 cal_err=+0.1815 brier=0.2280 BSS=-0.20 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-14T06:00:12]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=30 pred=0.4869 hit=0.4333 cal_err=+0.0535 brier=0.2321 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 2.71MB / last modified 2026-05-14T22:39:07.176621+09:00

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
26 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-14 22:35:06,626 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-14 22:35:06,697 [INFO] predictor: Models loaded OK
2026-05-14 22:35:06,708 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-14 22:36:05,424 [INFO] run_cycle: === run_cycle 22:36:05 ===
2026-05-14 22:36:05,424 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-14 22:36:05,424 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-14 22:36:05,466 [INFO] predictor: Models loaded OK
2026-05-14 22:36:05,470 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-14 22:37:06,641 [INFO] run_cycle: === run_cycle 22:37:06 ===
2026-05-14 22:37:06,642 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-14 22:37:06,642 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-14 22:37:06,693 [INFO] predictor: Models loaded OK
2026-05-14 22:37:06,697 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-14 22:38:05,851 [INFO] run_cycle: === run_cycle 22:38:05 ===
2026-05-14 22:38:05,851 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-14 22:38:05,851 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-14 22:38:05,926 [INFO] predictor: Models loaded OK
2026-05-14 22:38:05,936 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-14 22:39:06,690 [INFO] run_cycle: === run_cycle 22:39:06 ===
2026-05-14 22:39:06,690 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-14 22:39:06,690 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-14 22:39:06,738 [INFO] predictor: Models loaded OK
2026-05-14 22:39:06,742 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 76
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 76
  }
]
```

## Phase別通知記録 (24h)
{'final': 28, 'result': 16, 'scan': 32}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 79
  ANOMALY_SCRAPER_FAILURE_BURST: 43
  PSI_DRIFT_DETECTED: 31
  KS_ODDS_DRIFT: 30
  STRATEGY_CI_FAIL: 17
  LARGE_ODDS_DRIFT: 2
  ANOMALY_SCAN_FINAL_RATIO: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 51 | 15 | 15,300 | 13,230 | -2,070 | 0.865 |
| S01_NAKAANA1 | 35 | 14 | 7,000 | 5,620 | -1,380 | 0.803 |
| S02_TETSUBAN | 24 | 12 | 4,800 | 4,780 | -20 | 0.996 |
| S04_SELL_3T | 12 | 1 | 1,200 | 740 | -460 | 0.617 |

## 直近アラート (24h・新しい順)
```
[22:29:05] FINAL_MISSING: {"deadline": "2026-05-14T12:54:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051404031254", "sid": "S00"}
[22:27:06] FINAL_MISSING: {"deadline": "2026-05-14T09:50:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051423040950", "sid": "S00"}
[22:25:06] FINAL_MISSING: {"deadline": "2026-05-14T18:52:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051407081852", "sid": "S00"}
[22:25:06] FINAL_MISSING: {"deadline": "2026-05-14T11:48:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051403031148", "sid": "S00"}
[22:09:05] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.506}
[22:09:05] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 132, "n_recent": 110, "psi": 0.432}
[22:09:05] FINAL_MISSING: {"deadline": "2026-05-14T17:37:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051407051737", "sid": "S00"}
[22:07:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[21:59:05] FINAL_MISSING: {"deadline": "2026-05-14T18:27:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051407071827", "sid": "S00"}
[21:49:06] FINAL_MISSING: {"deadline": "2026-05-14T12:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051402041214", "sid": "S00"}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 168件 締切済
- 通知発射: scan=28 nid / final=27 nid / result=16 nid
- predictions: 16 / うち結果DB記録済: 16
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 8件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 0711R | win | 1 | 0.5990 | 2.2 | 1.32 | 200 | scan=2.2 drift=+0.0% | 20:08:46 |
| S02_TETSUBAN | 079R | win | 1 | 0.5123 | 2.0 | 1.02 | 200 | scan=- drift=- | 19:15:21 |
| S01_NAKAANA1 | 076R | win | 1 | 0.5123 | 4.0 | 2.05 | 200 | scan=4.6 drift=-13.0% | 17:59:22 |
| S01_NAKAANA1 | 074R | win | 1 | 0.5735 | 4.6 | 2.64 | 200 | scan=3.3 drift=+39.4% | 17:09:32 |
| S00 | 0410R | win | 1 | 0.5334 | 14.1 | 7.52 | 300 | scan=30.0 drift=-53.0% | 16:34:22 |
| S01_NAKAANA1 | 193R | win | 1 | 0.5123 | 3.4 | 1.74 | 200 | scan=4.3 drift=-20.9% | 16:25:21 |
| S02_TETSUBAN | 072R | win | 1 | 0.5334 | 2.2 | 1.17 | 200 | scan=2.3 drift=-4.3% | 16:00:30 |
| S00 | 121R | win | 1 | 0.4111 | 4.0 | 1.64 | 300 | scan=7.6 drift=-47.4% | 15:24:30 |
| S00 | 037R | win | 1 | 0.4111 | 4.8 | 1.97 | 300 | scan=4.7 drift=+2.1% | 13:39:32 |
| S02_TETSUBAN | 035R | win | 1 | 0.5014 | 2.2 | 1.10 | 200 | scan=- drift=- | 12:40:24 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| 3t | 12 | +11.6% | -41.4% | +75.7% | 5 | 1 | 9 |
| win | 72 | +3.8% | -75.4% | +522.0% | 28 | 16 | 46 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 462.0s |
| **Latency** (scan→final max) | 608.8s |
| **Traffic** (notifications 24h) | 76 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,100円 used |
| **Saturation** (S01_NAKAANA1) | 1,000円 used |
| **Saturation** (S02_TETSUBAN) | 800円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 242 | 0.4545 | 0.3017 | +0.1529 | 🟡+34% | 0.2324 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 183 | 0.4382 | 0.2568 | 0.2283 | 🔴-0.20 | 0.859 |
| S01_NAKAANA1 | win | 35 | 0.4969 | 0.4000 | 0.2378 | ✅+0.01 | 0.803 |
| S02_TETSUBAN | win | 24 | 0.5166 | 0.5000 | 0.2559 | 🔴-0.02 | 0.996 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 13 | 0.0030 | 0.0769 | 🔴-0.0739 |
| 0.15-0.20 | 7 | 0.1907 | 0.1429 | ✅+0.0479 |
| 0.20-0.30 | 10 | 0.2234 | 0.3000 | 🔴-0.0766 |
| 0.30-0.50 | 110 | 0.4259 | 0.2636 | 🔴+0.1623 |
| 0.50+ | 109 | 0.5410 | 0.3578 | 🔴+0.1832 |

## Settlement Ratio データ品質

- 学習済み: 3バンド / fallback: 14バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 12 | 0.821 |
| win | <5.0 | ✅learned | 27 | 0.718 |
| win | <10.0 | ✅learned | 25 | 0.564 |
| win | <20.0 | ⚠️fallback | 9 | 0.22 |
| win | <50.0 | ⚠️fallback | 0 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-05-14T22:40:01.407413+09:00_